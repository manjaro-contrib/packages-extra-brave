# Maintainer: Philip Müller <philm@manjaro.org>
# Contributor: Caleb Maclennan <caleb@alerque.com>
# Contributor: Jacob Mischka <jacob@mischka.me>
# Contributor: Manuel Mazzuola <origin.of@gmail.com>

pkgname=brave-beta
pkgver=0.66.90
pkgrel=1
pkgdesc='Web browser that blocks ads and trackers by default (latest binary release).'
arch=('x86_64')
url='https://github.com/brave/brave-browser/releases'
license=('custom')
depends=('gtk3' 'gconf' 'nss' 'alsa-lib' 'libxss' 'libgnome-keyring' 'ttf-font')
optdepends=('cups: Printer support'
            'pepper-flash: Adobe Flash support')
provides=('brave-browser')
conflicts=("${pkgname}-latest" 'brave-bin' 'brave-beta-bin' 'brave')
source=("brave-beta-$pkgver.zip::$url/download/v${pkgver}/brave-v${pkgver}-linux-x64.zip"
        'MPL2::https://raw.githubusercontent.com/brave/browser-laptop/master/LICENSE.txt'
        "brave.sh"
        "brave.desktop"
        "braveAbout.png")
options=(!strip)
sha512sums=('a2fcf0ac57c1114279af2b10fbf29cf5252f27e31912ce458761e5b9f559c32f72421461b7cb5cfc504bc270007bb8eb9dd34ee91cd5f8c4009ee8a094c658af'
            'b8823586fead21247c8208bd842fb5cd32d4cb3ca2a02339ce2baf2c9cb938dfcb8eb7b24c95225ae625cd0ee59fbbd8293393f3ed1a4b45d13ba3f9f62a791f'
            'd38e00c716a2789ca27c4dce86ab454552e156dd5048689f5800658b31e842c361dfa601ee70419c57b786194222e01f4be24c17f755e7e658b8c071ff097767'
            '400d345271a3c98be668e4aa08743d707647c92ee35951e937238ac07074119cfdb9601e1934cdf46014bd181b26ab0b568e4cab67c790efe53d029d8b0f9c55'
            'd7bef52e336bd908d24bf3a084a1fc480831d27a3c80af4c31872465b6a0ce39bdf298e620ae9865526c974465807559cc75610b835e60b4358f65a8a8ff159e')
noextract=("brave-beta-$pkgver.zip")

prepare() {
  mkdir -p brave
  cat brave-beta-$pkgver.zip | bsdtar -xf- -C brave
  chmod +x brave/brave
}

_bsdtardir="brave"

package() {
    install -d -m0755 "$pkgdir/usr/lib"
    cp -a --reflink=auto $_bsdtardir "$pkgdir/usr/lib/brave"

    install -Dm0755 "brave.sh" "$pkgdir/usr/bin/brave"
    install -Dm0644 -t "$pkgdir/usr/share/applications" "brave.desktop"
    install -Dm0644 "braveAbout.png" "$pkgdir/usr/share/pixmaps/brave.png"
    install -Dm0664 -t "$pkgdir/usr/share/licenses/brave" "MPL2"
    mv "$pkgdir/usr/lib/brave/"{LICENSE,LICENSES.chromium.html} "$pkgdir/usr/share/licenses/brave"

    ln -s /usr/lib/PepperFlash "$pkgdir/usr/lib/pepperflashplugin-nonfree"
}
