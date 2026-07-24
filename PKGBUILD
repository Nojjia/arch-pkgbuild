# Maintainer: Nojjia
pkgname=onlyoffice-desktopeditors-bin
pkgver=9.4.0
pkgrel=1
pkgdesc='An office suite that combines text, spreadsheet and presentation editors'
arch=(x86_64)
url='https://www.onlyoffice.com/'
license=('AGPL-3.0-only')
depends=(
	alsa-lib
	at-spi2-core
	cairo
	dbus
	expat
	fontconfig
	freetype2
	glib2
	glibc
	gst-plugins-base-libs
	gstreamer
	gtk3
	hicolor-icon-theme
	libcups
	libdrm
	libgcc
	libglvnd
	libice
	libnotify
	libpulse
	libsm
	libstdc++
	libx11
	libxcb
	libxcomposite
	libxdamage
	libxext
	libxfixes
	libxi
	libxkbcommon
	libxkbcommon-x11
	libxrandr
	mesa
	nspr
	nss
	pango
	qt5-base
	qt5-svg
	qt5-x11extras
	sh
	ttf-font
)
optdepends=('gst-plugins-ugly: support additional multimedia codecs')
conflicts=(onlyoffice-desktopeditors onlyoffice-desktopeditors-git onlyoffice onlyoffice-git only-office-bin)
options=(!debug !strip)
source=("https://github.com/ONLYOFFICE/DesktopEditors/releases/download/v${pkgver}/onlyoffice-desktopeditors-x64.tar.xz")
sha256sums=('d054d35f6c11274755cdad32683e8238f886420756c6cdcbf68c3b89ea66675c')

package() {
	local appdir="$pkgdir/opt/$pkgname"
	install -d "$appdir"

	# Install onlyoffice-desktopeditors-bin
	# Install to /opt instead of /usr/lib because this is a packaged binary
	cp -a "$srcdir/opt/onlyoffice/desktopeditors/." "$appdir"

	# Install desktop entry
	install -Dm644 "$srcdir/usr/share/applications/onlyoffice-desktopeditors.desktop" -t "$pkgdir/usr/share/applications/"

	# Install documentation
	install -Dm644 "$srcdir/usr/share/doc/onlyoffice-desktopeditors/ChangeLog" -t "$pkgdir/usr/share/doc/onlyoffice-desktopeditors/"
	install -Dm644 "$srcdir/usr/share/doc/onlyoffice-desktopeditors/NEWS" -t "$pkgdir/usr/share/doc/onlyoffice-desktopeditors/"

	# Install desktop icons
	for i in 16 24 32 48 64 128 256; do
		install -Dm644 "$srcdir/usr/share/icons/hicolor/${i}x${i}/apps/onlyoffice-desktopeditors.png" -t "$pkgdir/usr/share/icons/hicolor/${i}x${i}/apps/"
	done

	# Install licenses
	install -Dm644 "$srcdir/usr/share/licenses/onlyoffice-desktopeditors/3DPARTYLICENSE" -t "$pkgdir/usr/share/licenses/onlyoffice-desktopeditors/"
	install -Dm644 "$srcdir/usr/share/licenses/onlyoffice-desktopeditors/LICENSE" -t "$pkgdir/usr/share/licenses/onlyoffice-desktopeditors/"

	# Install launcher in /usr/bin
	install -Dm755 "$srcdir/usr/bin/onlyoffice-desktopeditors" -t "$pkgdir/usr/bin/"
}
