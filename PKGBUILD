# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Helmut Stult <helmut[at]manjaro[dot]org>
# Maintainer: Stefano Capitani <stefano[at]manjaro[dot]org>

# Arch credits:
# Mantainer: Andrés Rodríguez <hello@andres.codes>
# Contributor: Caleb Maclennan <caleb@alerque.com>
# Contributor: Jacob Mischka <jacob@mischka.me>
# Contributor: Manuel Mazzuola <origin.of@gmail.com>
# Contributor: Simón Oroño <simonorono@protonmail.com>
# Contributor: now-im <now im 627 @ gmail . com>
# Contributor: Giusy Digital <kurmikon at libero dot it>

_pkgname=brave
pkgname=$_pkgname-browser
pkgver=$(curl -s 'https://brave-browser-downloads.s3.brave.com/latest/release.version')
#pkgver=1.36.105
pkgrel=1
pkgdesc='Web browser that blocks ads and trackers by default (binary release)'
arch=(x86_64)
url=https://brave.com
license=(MPL2 BSD custom:chromium)
depends=(alsa-lib
         gtk3
         libxss
         nss
         ttf-font)
optdepends=('cups: Printer support'
            'libgnome-keyring: Enable GNOME keyring support'
            'libnotify: Native notification support')
provides=("${pkgname%-bin}=$pkgver")
conflicts=("${pkgname%-bin}")
options=(!strip)
source=("$pkgname-$pkgver.zip::https://github.com/brave/brave-browser/releases/download/v$pkgver/brave-browser-$pkgver-linux-amd64.zip"
        "$_pkgname.sh"
        'brave-browser.desktop')
noextract=("$pkgname-$pkgver.zip")
sha256sums=('8dd38353e71da481c9ad4d5cb93ca24ecac75cd3e8ae1e30b765cd34400525f7'
            '34814b275b51a4dac1c2aee8ee9ec2b6dbc1da32bc952a2a3147875e25965fc4'
            'c07276b69c7304981525ecb022f92daf7ae125a4fb05ac3442157b50826e257a')

prepare() {
	mkdir -p brave
	bsdtar -xf "$pkgname-$pkgver.zip" -C brave
	chmod +x brave/brave
}

package() {
	install -dm0755 "$pkgdir/usr/lib"
	cp -a brave "$pkgdir/usr/lib/$pkgname"

	# allow firejail users to get the suid sandbox working
	chmod 4755 "$pkgdir/usr/lib/$pkgname/chrome-sandbox"

	install -Dm0755 "$_pkgname.sh" "$pkgdir/usr/bin/brave"
	install -Dm0644 -t "$pkgdir/usr/share/applications/" "brave-browser.desktop"
	install -Dm0644 -t "$pkgdir/usr/share/licenses/$pkgname/" brave/LICENSE
	pushd "$pkgdir/usr/"
	for size in 16x16 24x24 32x32 48x48 64x64 128x128 256x256; do
		install -Dm0644 "lib/$pkgname/product_logo_${size/x*/}.png" \
			"share/icons/hicolor/$size/apps/brave-desktop.png"
	done
}
