# Maintainer: Nojjia

pkgname=zen-browser-bin
pkgver=1.21.5b
pkgrel=1
pkgdesc='Performance oriented Firefox-based web browser'
arch=('x86_64' 'aarch64')
url='https://zen-browser.app/'
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
provides=("${pkgname%-bin}=$pkgver")
conflicts=('zen-browser' 'zen-browser-git')
options=(!strip !debug)
install='zen-browser.install'
source_x86_64=("$pkgname-$pkgver-$pkgrel-x86_64.tar.xz::https://github.com/zen-browser/desktop/releases/download/$pkgver/zen.linux-$CARCH.tar.xz")
source_aarch64=("$pkgname-$pkgver-$pkgrel-aarch64.tar.xz::https://github.com/zen-browser/desktop/releases/download/$pkgver/zen.linux-$CARCH.tar.xz")
source=("${pkgname%-bin}.desktop")
sha256sums=('3fad64d11c1fbc015c024c5b3517fdbfab2f5585bd2ad0b1c39a805ae0ff791a')
sha256sums_x86_64=('0dea09bbc5fed9e1e32839f288a609b0b20eb1befed8d4f892e222a65dfaa069')
sha256sums_aarch64=('8178a85fca13ca1baf03c8c003ff833f4fae829a6b0e84d0111f28737f0c3b00')

package() {
	local appdir="$pkgdir/opt/$pkgname"
	install -d "$appdir"

	# Install zen
	#/opt instead of /usr/lib because this is a packaged binary
	cp -a zen/. "$appdir"

	# Install policies.json to disable auto-update
	install -Dvm644 /dev/stdin "$appdir/distribution/policies.json" <<END
{
	"policies": {
		"DisableAppUpdate": true,
		"AppAutoUpdate": false,
		"ManualAppUpdateOnly": true,
		"DefaultSerialGuardSetting": 3
	}
}
END

	# Symlink libonnxruntime
	# I think that the shipped libonnxruntime.so does nothing
	# and that the same approach as firefox package should be taken
	ln -srfv "$pkgdir/usr/lib/libonnxruntime.so" -t "$appdir"

	# Install desktop icons
	for i in 16 32 48 64 128; do
		install -Dvm644 "$appdir/browser/chrome/icons/default/default$i.png" "$pkgdir/usr/share/icons/hicolor/${i}x${i}/apps/${pkgname%-bin}.png"
	done
	
	# Install desktop file
	install -Dvm644 ../${pkgname%-bin}.desktop -t "$pkgdir/usr/share/applications/"

	# install a binary wrapper
	install -Dvm755 /dev/stdin "$pkgdir/usr/bin/${pkgname%-bin}" <<END
#!/bin/sh
exec /opt/$pkgname/zen "\$@"
END

	# Replace duplicate binary with wrapper
	ln -srfv "$pkgdir/usr/bin/${pkgname%-bin}" "$appdir/${pkgname/-browser/}"

	# Use system certificates
	ln -sfv /usr/lib/libnssckbi.so -t "$appdir"

	# Use system-provided dictionaries
	ln -Ts /usr/share/hunspell "$appdir/dictionaries"
	ln -Ts /usr/share/hyphen "$appdir/hyphenation"
}
