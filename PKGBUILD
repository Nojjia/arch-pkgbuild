# Maintainer: Nojjia

pkgname=zen-browser-bin
pkgver=1.21.6b
pkgrel=2
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
conflicts=('zen-browser' 'zen-browser-git')
options=(!strip !debug)
source_x86_64=("$pkgname-$pkgver-$pkgrel-x86_64.tar.xz::https://github.com/zen-browser/desktop/releases/download/$pkgver/zen.linux-x86_64.tar.xz")
source_aarch64=("$pkgname-$pkgver-$pkgrel-aarch64.tar.xz::https://github.com/zen-browser/desktop/releases/download/$pkgver/zen.linux-aarch64.tar.xz")
source=('zen.desktop')
sha256sums=('5ed53440b4a0505474058ee54f24924254e78ca4298e0f8e2a6dcec024167588')
sha256sums_x86_64=('eff490152c21b9a55b863b9df02370c30567e1027fe388eee939ed4082b53b20')
sha256sums_aarch64=('68df873f8b52c587a9d2fd9b46abc60c48d17e91741901ae2d0614f7ebe37469')

package() {
	local appdir="$pkgdir/opt/$pkgname"
	install -d "$appdir"

	# Install zen
	#/opt instead of /usr/lib because this is a packaged binary
	cp -a "$srcdir/zen/." "$appdir"

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
	# and that the same approach as firefox arch package should be taken
	ln -srfv "$pkgdir/usr/lib/libonnxruntime.so" -t "$appdir"

	# Install desktop icons
	for i in 16 32 48 64 128; do
		install -Dvm644 "$appdir/browser/chrome/icons/default/default$i.png" "$pkgdir/usr/share/icons/hicolor/${i}x${i}/apps/${pkgname%-bin}.png"
	done
	
	# Install desktop file
	install -Dvm644 "$srcdir/zen.desktop" -t "$pkgdir/usr/share/applications/"

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
