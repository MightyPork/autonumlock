# Maintainer: Ondrej Hruska <ondra@ondrovo.com>

_pkgname="autonumlock"
pkgname="autonumlock-git"

pkgver=0799a5a
pkgrel=1

pkgdesc="Script for watching for external keyboard and enabling numlock when connected. Useful for laptops that lack numeric block. Can also be used to alter keyboard layout and run arbitrary scripts, using the config file."
arch=("any")
url="https://github.com/MightyPork/autonumlock"
license=("MIT")

depends=(bash usbutils numlockx)

makedepends=("git")

source=("git+https://github.com/MightyPork/autonumlock.git")
provides=($_pkgname)
replaces=($_pkgname)
md5sums=("SKIP")

pkgver() {
	cd "${srcdir}/${_pkgname}"
	git describe --always | sed 's|-|.|g'
}

package() {
	# install license
	install -Dm 644 "${srcdir}/${_pkgname}/LICENSE" "${pkgdir}/usr/share/licenses/${_pkgname}/LICENSE"

	mkdir "${pkgdir}/usr/share/${_pkgname}/"

	cp -p "${srcdir}/${_pkgname}"/* "${pkgdir}/usr/share/${_pkgname}/"

	ln -s /usr/share/${pkgname}/autonumlock "${pkgdir}/usr/bin/adios"
}
