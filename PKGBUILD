# Maintainer: Nojjia

## Package name
pkgname=zen-browser-git

## Version
pkgver=0
pkgrel=1

## Generic
pkgdesc="Beautifully designed, privacy-focused, and packed with features. "
arch=(x86_64)
url="https://zen-browser.app/"
license=('MPL-2.0')
groups=()

## Dependencies
depends=()
makedepends=(base-devel git curl python python-pip libvips sccache)
#checkdepends=()
optdepends=()

## Package relations
provides=("${pkgname%-VCS}")
conflicts=("${pkgname%-VCS}")
replaces=()

## Others
backup=()
options=()
install=
#changelog=

## Sources
source=('zen-browser::git+https://github.com/zen-browser/desktop.git#branch=stable')
noextract=()
#validpgpkeys=()

## Integrity
sha256sums=('SKIP')

# Please refer to the 'USING VCS SOURCES' section of the PKGBUILD man page for
# a description of each element in the source array.

pkgver() {
	cd "$srcdir/${pkgname%-VCS}"
# Git, tags available
	printf "%s" "$(git describe --long | sed 's/\([^-]*-\)g/r\1/;s/-/./g')"
}

prepare() {
	git clone https://github.com/zen-browser/desktop.git --depth 5
	cd "$srcdir/${pkgname%-VCS}"
	npm i
	npm run init
	python3 ./scripts/update_en_US_packs.py
}

build() {
	cd "$srcdir/${pkgname%-VCS}"
	make
}

check() {
	cd "$srcdir/${pkgname%-VCS}"
	make -k check
}

package() {
	cd "$srcdir/${pkgname%-VCS}"
	make DESTDIR="$pkgdir/" install
}
