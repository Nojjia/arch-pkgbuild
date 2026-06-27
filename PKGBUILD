# Maintainer: Nojjia <youremail@domain.com>

## Custom Set Variables
_vcs=git

## Package Name
pkgname=dwm

## Package Version
pkgver=r3.3bd597b
pkgrel=1
#epoch= #!Should not be used!

## Generic
pkgdesc="Dynamic Window Manager - Nojjia's Roll"
arch=(x86_64)
url="https://github.com/Nojjia/dwm"
license=('MIT')
#groups=()

## Dependencies
depends=(
	libx11
	libxinerama
	fontconfig
	libxft
) #Package name
makedepends=($_vcs)
#checkdepends=()
optdepends=(
	'rofi: A window switcher, application launcher and dmenu replacement'
	'alacritty: A cross-platform, GPU-accelerated terminal emulator'
	'dolphin: KDE File Manager'
	'zen-browser: Performance oriented Firefox-based web browser'
	'firefox: Fast, Private & Safe Web Browser'
	'kalk: A powerful cross-platform calculator application built with the Kirigami framework'
	'brightnessctl: Lightweight brightness control tool'
	'wireplumber: Session / policy manager implementation for PipeWire'
	'playerctl: mpris media player controller and lib for spotify, vlc, audacious, bmp, xmms2, and others.'
	)

## Package Relations
provides=("${pkgname}")
conflicts=("${pkgname}")
#replaces=()

## Others
#backup=()
options=(strip zipman !debug lto)
#install=dwm.install
#changelog=

## Sources
source=("$pkgname::$_vcs+$url.git")
#noextract=()
#validpgpkeys=()

## Integrity
sha256sums=('SKIP')

pkgver() {
	cd "$srcdir/${pkgname}"

# Git, tags available
#	printf "%s" "$(git describe --long | sed 's/\([^-]*-\)g/r\1/;s/-/./g')"

# Git, no tags available
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"

}

prepare() {
	cd "$srcdir/${pkgname}"
}

build() {
	cd "$srcdir/${pkgname}"
	make
}

#check() {
#	cd "$srcdir/${pkgname}"
#	make -k check
#}

package() {
	cd "$srcdir/${pkgname}"
	make PREFIX=/usr DESTDIR="$pkgdir/" install
	install -Dm644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}/"
	install -Dm644 dwm.desktop -t "${pkgdir}/usr/share/xsessions/"
}
