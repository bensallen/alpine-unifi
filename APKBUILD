# Contributor:
# Maintainer:
pkgname=unifi
pkgver=5.4.16
pkgrel=0
pkgdesc="UniFi Controller"
url="https://www.ubnt.com/enterprise/software/"
arch="x86_64"
license="custom"
depends="mongodb openjdk8-jre-base"
makedepends=""
install=""
subpackages="$pkgname-doc $pkgname-firmware:firmware:noarch"
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
	rm -rf "$pkgdir"/lib "$pkgdir"/etc/init.d/unifi "$pkgdir"/usr/lib/unifi/lib/native/Mac "$pkgdir"/usr/lib/unifi/lib/native/Windows "$pkgdir"/usr/lib/unifi/lib/native/Linux/armhf/libubnt_webrtc_jni.so

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

sha512sums="e363c38b188280a0cf0d1a99f7a6d9bf659e173619218169a7cf3ecbcfaa54650da275ff781a099b9a1fc64bf236a7358931a5df5a385c6b8af4f33ce15e6d9c  unifi-5.4.16.deb
c2fdcfa6ff596afeb1feb25a6c06f4ebc79a266b784e4ab3b6c97379179286c95c2070529bc1b83fedf2f19f768b170a952230596e4c8c9eb87c46d4ac4d9946  unifi.initd
0bce21316834d423c0bbebb5d4513bbd6d0ecc7ea99e34487da9955fcab71ec9a5f5cd93c896192868a8fc5e5c585e3b01d623d2f835d163f47e221a0688c3d1  unifi.confd"
