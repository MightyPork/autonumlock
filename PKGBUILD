# Maintainer: Ondrej Hruska <ondra@ondrovo.com>

_pkgname="autonumlock"
pkgname="autonumlock-git"

pkgver=1.0.0
pkgrel=1

pkgdesc="Script for watching for external keyboard and enabling numlock when connected. Useful for laptops that lack numeric block."
arch=("any")
url="https://github.com/MightyPork/autonumlock"
license=("MIT")

depends=("bash usbutils numlockx")

makedepends=("git")

source=("git+https://github.com/MightyPork/autonumlock.git")
provides=($_pkgname)
replaces=($_pkgname)
md5sums=("SKIP")

pkgver() {
	cd "${srcdir}/${_pkgname}"
	git describe --tags | sed "s|-|.|g"
}

package() {
	# install license
	install -Dm 644 "${srcdir}/${_pkgname}/LICENSE" "${pkgdir}/usr/share/licenses/${_pkgname}/LICENSE"
	install -Dm 755 "${srcdir}/${_pkgname}/autonumlock" "${pkgdir}/usr/bin/autonumlock"
}
