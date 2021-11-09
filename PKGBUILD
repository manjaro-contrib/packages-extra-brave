# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Helmut Stult <helmut[at]manjaro[dot]org>
# Maintainer: Stefano Capitani <stefano[at]manjaro[dot]org>

# Arch credits:
# Maintainer: Greg White <gwhite@kupulau.com>

_pkgname=brave
pkgname=$_pkgname-browser-beta
pkgver=$(echo $(curl -s 'https://brave-browser-downloads.s3.brave.com/latest/beta.version'))
pkgrel=1
pkgdesc='Web browser that blocks ads and trackers by default (latest binary release).'
arch=('x86_64')
url='https://github.com/brave/brave-browser/releases'
license=("MPL2" "BSD" "custom:chromium")
depends=("gtk3" "nss" "alsa-lib" "libxss" "ttf-font")
optdepends=("cups: Printer support"
            "pepper-flash: Adobe Flash support"
            "libgnome-keyring: Enable GNOME keyring support")
makedepends=('curl')
provides=("${_pkgname%-bin}" "brave-browser" "brave")
conflicts=("${_pkgname%-bin}" "brave" "$_pkgname" 'brave-beta-browser')
replaces=("$_pkgname" 'brave-beta-browser')
source=("${_pkgname}-${pkgver}.zip::https://github.com/brave/brave-browser/releases/download/v${pkgver}/brave-browser-beta-${pkgver}-linux-amd64.zip"
        "LICENSE::https://raw.githubusercontent.com/brave/brave-browser/master/LICENSE"
        "$_pkgname-beta.sh"
        "brave-browser.desktop")
options=(!strip)
sha256sums=('1b0294e994d7ba7482bc6ff00a9f3d2082c4ec22e417a6eeda989be2ddf87727'
            '3f3d9e0024b1921b067d6f7f88deb4a60cbe7a78e76c64e3f1d7fc3b779b9d04'
            'cfcdb2afe2ecf1c5ec786fff57c6aca84f42a101807143da3e4ae620d7235dff'
            '76d0c74c6676b6e579c37c41846140bc76a86e27c5cabd21bc9ae4c4c505cf60')
noextract=("$_pkgname-$pkgver.zip")

prepare() {
  mkdir -p brave
  cat $_pkgname-$pkgver.zip | bsdtar -xf- -C brave
  chmod +x brave/brave
}

_bsdtardir="brave"

package() {
    install -d -m0755 "$pkgdir/usr/lib"
    cp -a --reflink=auto $_bsdtardir "$pkgdir/usr/lib/$_pkgname"
    # see https://github.com/brave/brave-browser/issues/17122
	chmod 755 "$pkgdir/usr/lib/$_pkgname/chrome_crashpad_handler"

    install -Dm0755 "$_pkgname-beta.sh" "$pkgdir/usr/bin/brave"
    install -Dm0644 -t "$pkgdir/usr/share/applications" "brave-browser.desktop"
    install -Dm0664 -t "${pkgdir}/usr/share/licenses/${_pkgname}" "LICENSE"
    ln -s /usr/lib/PepperFlash "${pkgdir}/usr/lib/pepperflashplugin-nonfree"
    mkdir "$pkgdir/usr/share/pixmaps"
    ln -s "$pkgdir/usr/lib/brave/product_logo_128_beta.png" "$pkgdir/usr/share/pixmaps/brave-desktop.png"
}
