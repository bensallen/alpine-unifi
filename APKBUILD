# Contributor:
# Maintainer:
pkgname=unifi
pkgver=5.4.9
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

md5sums="5a0cadeb19fbeaa8ebeae4c3f0c6e26c  unifi_sysvinit_all.deb
fdc9a625a4a9931263ba1ebb17dda35e  unifi.initd
46e6f22c4aee39d6bbe724e1661cbb3d  unifi.confd"
sha256sums="e24d45c3e46f2cf717db8358d8bd7dc15bee9d20aeef4ba67b668d45f3d34f4f  unifi_sysvinit_all.deb
e567298b39f9b97bfcaf7c86a3687b101b9c11ee1794596b41b8fab91d4bade2  unifi.initd
6783cbb32f771f2559fd20d60c35ca7213079fbacabf68cc14b1c673614bcc0e  unifi.confd"
sha512sums="be7a3b2a6ffee50a1711cabc1980577a7bbaa909c48a798b441a9bd21f7c7676814cdd8399d5fd96b7f3a32c0d642a7279f91fc67e0611dd8f51a2f28f642f45  unifi_sysvinit_all.deb
c2fdcfa6ff596afeb1feb25a6c06f4ebc79a266b784e4ab3b6c97379179286c95c2070529bc1b83fedf2f19f768b170a952230596e4c8c9eb87c46d4ac4d9946  unifi.initd
0bce21316834d423c0bbebb5d4513bbd6d0ecc7ea99e34487da9955fcab71ec9a5f5cd93c896192868a8fc5e5c585e3b01d623d2f835d163f47e221a0688c3d1  unifi.confd"
