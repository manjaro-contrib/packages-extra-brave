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

pkgname=brave
pkgver=1.26.77
pkgrel=1
pkgdesc='Web browser that blocks ads and trackers by default (latest binary release).'
arch=('x86_64')
url='https://brave.com/download'
license=("MPL2" "BSD" "custom:chromium")
depends=("gtk3" "nss" "alsa-lib" "libxss" "ttf-font")
optdepends=("cups: Printer support"
            "pepper-flash: Adobe Flash support"
            "libgnome-keyring: Enable GNOME keyring support")
makedepends=('curl')
provides=("${pkgname%-bin}" "brave-browser")
conflicts=("${pkgname%-bin}")
source=("$pkgname-$pkgver.zip::https://github.com/brave/brave-browser/releases/download/v${pkgver}/brave-browser-${pkgver}-linux-amd64.zip"
        "$pkgname.sh"
        "brave-browser.desktop"
        "logo.png")
options=(!strip)
sha256sums=('386e0b3d5dcb2a4ff5effc39df1f3f76bac2b9e7623d141e0f39f97f5659affa'
            'cfcdb2afe2ecf1c5ec786fff57c6aca84f42a101807143da3e4ae620d7235dff'
            '76d0c74c6676b6e579c37c41846140bc76a86e27c5cabd21bc9ae4c4c505cf60'
            '4a585cb8740f4c9ba267f0df19d894eb9fae1b9a6af4a3e44737b7d0bcbc104a')
noextract=("$pkgname-$pkgver.zip")

pkgver() {
  curl -s "https://api.github.com/repos/brave/brave-browser/releases?page=1&per_page=100" | jq -r '.[] | select( .prerelease == false and .draft == false ) | select(all( .name; contains("Nightly") | not ))  | select(all( .name; contains("Beta") | not )) | select(all( .body; contains("unstable") | not )) | {name: .name, url: .url, tarball_url: .tarball_url, published_at: .published_at}' | jq --slurp '.[0]' | grep "Release" |  cut -d 'v' -f2 | cut -d '"' -f1
}

prepare() {
  mkdir -p brave
  cat $pkgname-$pkgver.zip | bsdtar -xf- -C brave
  chmod +x brave/brave
}

_bsdtardir="brave"

package() {
    install -d -m0755 "$pkgdir/usr/lib"
    cp -a --reflink=auto $_bsdtardir "$pkgdir/usr/lib/$pkgname"

    install -Dm0755 "$pkgname.sh" "$pkgdir/usr/bin/brave"
    install -Dm0644 -t "$pkgdir/usr/share/applications" "brave-browser.desktop"
    install -Dm0644 "logo.png" "$pkgdir/usr/share/pixmaps/brave-desktop.png"
    LICENSES_DIR="$pkgdir/usr/share/licenses/$pkgname"
    mkdir -p "$LICENSES_DIR"
    if [ -f "$pkgdir/usr/lib/$pkgname/LICENSE" ] && [ -f "$pkgdir/usr/lib/$pkgname/LICENSES.chromium.html" ]; then
      mv "$pkgdir/usr/lib/$pkgname/"{LICENSE,LICENSES.chromium.html} "$LICENSES_DIR"
    fi

}
