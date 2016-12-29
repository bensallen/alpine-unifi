# Contributor:
# Maintainer:
pkgname=unifi
pkgver=5.3.8
pkgrel=0
pkgdesc="UniFi Controller"
url="https://www.ubnt.com/enterprise/software/"
arch="x86_64"
license="custom"
depends="mongodb openjdk8-jre-base"
makedepends=""
install=""
subpackages="$pkgname-doc $pkgname-firmware"
source="http://dl.ubnt.com/unifi/${pkgver}/unifi_sysvinit_all.deb $pkgname.initd $pkgname.confd"
builddir="$srcdir/"
prepare() {
	cd "$builddir"
	# Extract the deb
	ar -x unifi_sysvinit_all.deb
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
	rm -rf "$pkgdir"/lib "$pkgdir"/etc/init.d/unifi

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

md5sums="0d896fdc8fe378636e2a397c9e76922d  unifi_sysvinit_all.deb
fdc9a625a4a9931263ba1ebb17dda35e  unifi.initd
46e6f22c4aee39d6bbe724e1661cbb3d  unifi.confd"
sha256sums="2d80ccf466c3c74e0078960ac0ce0fd57046f0500e98a0caad5b6a450565f872  unifi_sysvinit_all.deb
e567298b39f9b97bfcaf7c86a3687b101b9c11ee1794596b41b8fab91d4bade2  unifi.initd
6783cbb32f771f2559fd20d60c35ca7213079fbacabf68cc14b1c673614bcc0e  unifi.confd"
sha512sums="a15e9da5b450469c6afda110b9b577ee6d6a2f57a7560f2c5a4d6d56ca5d53b8311293dce9e6237abbeacf632a570e9c5a3bc9ebf08b3764202e414a20854f58  unifi_sysvinit_all.deb
c2fdcfa6ff596afeb1feb25a6c06f4ebc79a266b784e4ab3b6c97379179286c95c2070529bc1b83fedf2f19f768b170a952230596e4c8c9eb87c46d4ac4d9946  unifi.initd
0bce21316834d423c0bbebb5d4513bbd6d0ecc7ea99e34487da9955fcab71ec9a5f5cd93c896192868a8fc5e5c585e3b01d623d2f835d163f47e221a0688c3d1  unifi.confd"
