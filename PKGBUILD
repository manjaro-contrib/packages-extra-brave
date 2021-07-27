# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Helmut Stult <helmut[at]manjaro[dot]org>
# Maintainer: Stefano Capitani <stefano[at]manjaro[dot]org>

# Arch credits:
# Maintainer: Greg White <gwhite@kupulau.com>

_pkgname=brave-beta
pkgname=$_pkgname-browser
_pkgver=$(echo $(curl -s 'https://brave-browser-downloads.s3.brave.com/latest/beta.version'))
pkgver=1.28.92
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
conflicts=("${_pkgname%-bin}" "brave" "$_pkgname")
replaces=("$_pkgname")
source=("${_pkgname}-${_pkgver}.zip::https://github.com/brave/brave-browser/releases/download/v${_pkgver}/brave-browser-beta-${_pkgver}-linux-amd64.zip"
        "LICENSE::https://raw.githubusercontent.com/brave/brave-browser/master/LICENSE"
        "$_pkgname.sh"
        "brave-browser.desktop"
        "logo.png")
options=(!strip)
sha256sums=('c357a506a0e258dcc2d77092d8d729de0a87d407f4aabd807eae225893be8fe6'
            '3f3d9e0024b1921b067d6f7f88deb4a60cbe7a78e76c64e3f1d7fc3b779b9d04'
            'ae44455a9ce06c68eec22ade43815d8a809d7fde3e90a950400e2ba7da6a7560'
            '76d0c74c6676b6e579c37c41846140bc76a86e27c5cabd21bc9ae4c4c505cf60'
            '4a585cb8740f4c9ba267f0df19d894eb9fae1b9a6af4a3e44737b7d0bcbc104a')
noextract=("$_pkgname-$_pkgver.zip")

pkgver() {
  echo $(curl -s 'https://brave-browser-downloads.s3.brave.com/latest/beta.version')
}

prepare() {
  mkdir -p brave
  cat $_pkgname-$_pkgver.zip | bsdtar -xf- -C brave
  chmod +x brave/brave
}

_bsdtardir="brave"

package() {
    install -d -m0755 "$pkgdir/usr/lib"
    cp -a --reflink=auto $_bsdtardir "$pkgdir/usr/lib/$_pkgname"

    install -Dm0755 "$_pkgname.sh" "$pkgdir/usr/bin/brave"
    install -Dm0644 -t "$pkgdir/usr/share/applications" "brave-browser.desktop"
    install -Dm0644 "logo.png" "$pkgdir/usr/share/pixmaps/brave-desktop.png"
    install -Dm0664 -t "${pkgdir}/usr/share/licenses/${_pkgname}" "LICENSE"
    ln -s /usr/lib/PepperFlash "${pkgdir}/usr/lib/pepperflashplugin-nonfree"
}
