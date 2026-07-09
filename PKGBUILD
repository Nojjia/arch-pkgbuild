# Maintainer: Nojjia

pkgname=zen-browser
pkgver=1.21.6b
pkgrel=1
pkgdesc="Performance oriented Firefox-based web browser"
arch=('x86_64' 'aarch64')
url="https://zen-browser.app/"
license=('MPL-2.0')
groups=(browsers)
depends=(
	alsa-lib
	at-spi2-core
	cairo
	dbus
	fontconfig
	freetype2
	gdk-pixbuf2
	glib2
	glibc
	gtk3
	hicolor-icon-theme
	libgcc
	libstdc++
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
	mime-types
	nspr
	nss
	pango
	ttf-font
)
makedepends=(
	base-devel
	curl
	python
	python-pip
	libvips
	sccache)
checkdepends=()
optdepends=(
	'hunspell: Spell checking, American English'
	'hyphen: hyphenation support'
	'libnotify: Notification integration'
	'libva: Hardware video acceleration'
	'networkmanager: Location detection via available WiFi networks'
	'onnxruntime: Local machine learning features such as smart tab groups'
	'pipewire-pulse: Audio support through PipeWire'
	'speech-dispatcher: Text-to-Speech'
	'xdg-desktop-portal: Screensharing with Wayland'
	'ffmpeg: Additional media format support'
)
conflicts=('zen-browser-bin' 'zen-browser-git')
options=(!lto !emptydirs !makeflags)
source=("https://github.com/zen-browser/desktop/releases/download/$pkgver/zen.source.tar.zst")
sha256sums=('5b9229c1c5f9a2383a4699df636ddd4c6b81d5b7a3cfe3bdb1a79e65a9ddec9e')

prepare() {
	# Install Dependencies
	#npm i

	# Download and Bootstrap the Browser
	#npm run init

	# Update Language Packs
	#python3 ./scripts/update_en_US_packs.py
}

build() {
	# Build the Browser
	npm run build
}

check() {
}

package() {
}
