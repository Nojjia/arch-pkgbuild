# Maintainer: Nojjia
pkgname=arduino-ide-v2-bin
pkgver=2.3.10
pkgrel=1
pkgdesc='Arduino prototyping platform IDE, rewrite based on the Theia IDE framework.'
arch=(x86_64)
url='https://arduino.cc/'
license=('AGPL-3.0-or-later')
groups=(ide)
depends=(
	alsa-lib
	at-spi2-core
	cairo
	dbus
	expat
	glib2
	glibc
	gtk3
	libcups
	libdrm
	libgcc
	libsecret
	libstdc++
	libx11
	libxcb
	libxcomposite
	libxdamage
	libxext
	libxfixes
	libxkbcommon
	libxkbfile
	libxrandr
	mesa
	nspr
	nss
	pango
)
optdepends=(
	'libusb: Needed for some libraries or boards'
	'usbutils: Needed for stm32 boards using st-link'
	'libusb-compat: Needed for the `micronucleus` cli utility'
	'python-pyserial: Needed for esptool'
)
conflicts=(arduino-ide arduino-ide-git)
options=(!debug !strip)
source=("https://github.com/arduino/arduino-ide/releases/download/2.3.10/arduino-ide_${pkgver}_Linux_64bit.zip"
)
sha256sums=('cc8a0b01e763d4646b670ce70c1bc8c389a0fa14ab556dcc0749c03f475a7975')

prepare() {
	rm -rf "$srcdir/arduino-ide_${pkgver}_Linux_64bit/resources/app/plugins/cortex-debug/extension/binary_modules/v12.14.1/win32"
	rm -rf "$srcdir/arduino-ide_${pkgver}_Linux_64bit/resources/app/plugins/cortex-debug/extension/binary_modules/v12.18.3"
	rm -rf "$srcdir/arduino-ide_${pkgver}_Linux_64bit/resources/app/plugins/cortex-debug/extension/binary_modules/v12.14.1/darwin"

	rm -rf "$srcdir/arduino-ide_${pkgver}_Linux_64bit/resources/app/plugins/cortex-debug/extension/binary_modules/v12.14.1/linux/arm"
	rm -rf "$srcdir/arduino-ide_${pkgver}_Linux_64bit/resources/app/plugins/cortex-debug/extension/binary_modules/v12.14.1/linux/arm64"
}

package() {
	local appdir="$pkgdir/opt/$pkgname"
	install -d "$appdir"

	# Install arduino-ide-v2
	# Install to /opt instead of /usr/lib because this is a packaged binary
	cp -a "$srcdir/arduino-ide_${pkgver}_Linux_64bit/." "$appdir"

	# Install desktop icons
	install -Dm644 "$appdir/resources/app/resources/icons/512x512.png" "$pkgdir/usr/share/icons/hicolor/512x512/apps/${pkgname%-bin}.png"

	# Install desktop entry
	install -Dm644 /dev/stdin "$pkgdir/usr/share/applications/${pkgname%-bin}.desktop" <<EOF
[Desktop Entry]
Name=Arduino IDE 2.x
Comment=Opensource electronics prototyping platform
Exec=arduino-ide-v2 %u
Icon=arduino-ide-v2
Type=Application
StartupWMClass=arduino-ide-v2
Categories=Development;IDE;Electronics;
StartupNotify=true
Terminal=false
GenericName=Arduino IDE 2.x
Keywords=embedded electronics;avr;microcontroller;
MimeType=text/x-arduino;
EOF

	install -Dm755 /dev/stdin "$pkgdir/usr/bin/${pkgname%-bin}" <<EOF
#!/bin/sh
exec /opt/arduino-ide-v2-bin/arduino-ide "$@"
EOF
}
