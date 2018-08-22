# Contributor:
# Maintainer:
pkgname=unifi
pkgver=5.8.28
pkgrel=0
pkgdesc="UniFi Controller"
url="https://www.ubnt.com/enterprise/software/"
arch="x86_64"
license="custom"
depends="mongodb openjdk8-jre-base gcompat"
makedepends=""
install=""
subpackages="$pkgname-openrc $pkgname-doc $pkgname-firmware:firmware:noarch"
source="$pkgname-$pkgver.deb::http://dl.ubnt.com/unifi/${pkgver}/unifi_sysvinit_all.deb $pkgname.initd $pkgname.confd"
builddir="$srcdir/"
options="!check"
prepare() {
	cd "$builddir"
	# Extract the deb
	ar -x $pkgname-$pkgver.deb
}
build() {
	cd "$builddir"
}

package() {
	cd "$builddir"
	mkdir -p "$pkgdir"

	# Extract the data portion of the Deb
	tar -C "$pkgdir" -xf data.tar.xz

	# Remove uneeded files
	rm -rf "$pkgdir"/lib "$pkgdir"/etc/init.d/unifi "$pkgdir"/usr/lib/unifi/lib/native/Mac "$pkgdir"/usr/lib/unifi/lib/native/Windows "$pkgdir"/usr/lib/unifi/lib/native/Linux/x86_64/libubnt_sdnotify_jni.so "$pkgdir"/usr/lib/unifi/lib/native/Linux/armhf "$pkgdir"/usr/lib/unifi/lib/native/Linux/armv7 "$pkgdir"/usr/lib/unifi/lib/native/Linux/aarch64

	install -dDm755 "$pkgdir"/var/log/unifi
	install -dDm755 "$pkgdir"/var/run/unifi
	install -dDm755 "$pkgdir"/var/lib/unifi

	# Symlink in directories to where UniFi expects them
	ln -s /usr/bin/mongod "$pkgdir"/usr/lib/unifi/bin/mongod
	ln -s /var/lib/unifi "$pkgdir"/usr/lib/unifi/data
	ln -s /var/log/unifi "$pkgdir"/usr/lib/unifi/logs
	ln -s /var/run/unifi "$pkgdir"/usr/lib/unifi/run

	# Install init script
	install -Dm755 "$srcdir"/unifi.initd "$pkgdir"/etc/init.d/unifi
	install -Dm644 "$srcdir"/unifi.confd "$pkgdir"/etc/conf.d/unifi
}


firmware() {
	mkdir -p "$subpkgdir"/usr/lib/unifi/dl
	mv "$pkgdir"/usr/lib/unifi/dl/firmware "$subpkgdir"/usr/lib/unifi/dl/firmware
}

sha512sums="9f2679f4e95ee64732a1d278a47bebbf993030a2ca254a43e9b2e9b5c9bcbe011eefda4f55526afec44f82b1fa3279df1162b47de013efc9d1354a5237651206  unifi-5.8.28.deb
c490f7ba0da084992667370607091ca607746231707237b133b45453c02974c5be958eede530d3a69aee536b413ad38b0b1e1ca6d0ba9a3dfbf7fc0010e04d1f  unifi.initd
0bce21316834d423c0bbebb5d4513bbd6d0ecc7ea99e34487da9955fcab71ec9a5f5cd93c896192868a8fc5e5c585e3b01d623d2f835d163f47e221a0688c3d1  unifi.confd"
