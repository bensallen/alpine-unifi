# Contributor:
# Maintainer:
pkgname=unifi
pkgver=5.4.11
pkgrel=0
pkgdesc="UniFi Controller"
url="https://www.ubnt.com/enterprise/software/"
arch="x86_64"
license="custom"
depends="mongodb openjdk8-jre-base"
makedepends=""
install=""
subpackages="$pkgname-doc $pkgname-firmware"
source="$pkgname-$pkgver.deb::http://dl.ubnt.com/unifi/${pkgver}/unifi_sysvinit_all.deb $pkgname.initd $pkgname.confd"
builddir="$srcdir/"
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

md5sums="821c9d2b50ae413f00b2ffb502c81176  unifi-5.4.11.deb
fdc9a625a4a9931263ba1ebb17dda35e  unifi.initd
46e6f22c4aee39d6bbe724e1661cbb3d  unifi.confd"
sha256sums="131560f4d7d5273c82b4124125991ca823c79434eeae7f2c60b9293c094da658  unifi-5.4.11.deb
e567298b39f9b97bfcaf7c86a3687b101b9c11ee1794596b41b8fab91d4bade2  unifi.initd
6783cbb32f771f2559fd20d60c35ca7213079fbacabf68cc14b1c673614bcc0e  unifi.confd"
sha512sums="457bc0f068c2a56c99bea7b084b0580e708148cf5db610670bf2630c420939c23ed07632d6b33f681e430a3779d96d52f736cde3aec4d875eea2555bdfc68a5a  unifi-5.4.11.deb
c2fdcfa6ff596afeb1feb25a6c06f4ebc79a266b784e4ab3b6c97379179286c95c2070529bc1b83fedf2f19f768b170a952230596e4c8c9eb87c46d4ac4d9946  unifi.initd
0bce21316834d423c0bbebb5d4513bbd6d0ecc7ea99e34487da9955fcab71ec9a5f5cd93c896192868a8fc5e5c585e3b01d623d2f835d163f47e221a0688c3d1  unifi.confd"
