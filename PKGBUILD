# Maintainer: Nojjia

## Package name
pkgname=zen-browser-stable-git

## Version
pkgver=0
pkgrel=1

## Generic
pkgdesc="Beautifully designed, privacy-focused, and packed with features. Stable release"
arch=(x86_64)
url="https://zen-browser.app/"
license=('MPL-2.0')
groups=()

## Dependencies
depends=(
	alsa-lib
	cairo
	dbus
	firefox
	fontconfig
	freetype2
	gcc
	glibc
	gtk3
	libtasn1
	libx11
	libxcb
	libxcomposite
	libxcursor
	libxdamage
	libxext
	libxfixes
	libxi
	libxrandr
	libxrender
	nspr
	nss
	)
makedepends=(base-devel git curl python python-pip libvips sccache)
#checkdepends=()
optdepends=(
	hunspell-en_US
	libnotify
	networkmanager
	onnxruntime
	speech-dispatcher
	xdg-desktop-portal
	)

## Package relations
provides=("${pkgname%-VCS}")
conflicts=("${pkgname%-VCS}")
replaces=()

## Others
#backup=()
options=(strip zipman !debug lto)
install=zen-browser.install
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
