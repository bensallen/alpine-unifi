# Contributor:
# Maintainer:
pkgname=unifi
pkgver=5.5.24
pkgrel=0
pkgdesc="UniFi Controller"
url="https://www.ubnt.com/enterprise/software/"
arch="x86_64"
license="custom"
depends="mongodb openjdk8-jre-base gcompat"
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

sha512sums="cd5de5e9952b07afa458ff9b7f5f025f88212a15aaa7381a78aeba1e6909b7e2e52b3305fee45e8fe2dbd7c308897a58e1248afb1726f57829a9e05f7ecaa7a4  unifi-5.5.24.deb
7cfd1b9721392e2508f3d8203040ec14cf5c52f1741c57bd5ef6ad8c215bf0fcf9ce8b5f7fbceb88d263f7b5e53da79cce737e2020ec7be4669ae64a4228074b  unifi.initd
0bce21316834d423c0bbebb5d4513bbd6d0ecc7ea99e34487da9955fcab71ec9a5f5cd93c896192868a8fc5e5c585e3b01d623d2f835d163f47e221a0688c3d1  unifi.confd"
