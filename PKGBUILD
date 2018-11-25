# Maintainer: Philip Müller <philm@manjaro.org>
# Contributor: Caleb Maclennan <caleb@alerque.com>
# Contributor: Jacob Mischka <jacob@mischka.me>
# Contributor: Manuel Mazzuola <origin.of@gmail.com>

pkgname=brave
pkgver=0.56.15
pkgrel=1
pkgdesc='Web browser that blocks ads and trackers by default (latest binary release).'
arch=('x86_64')
url='https://brave.com/download'
license=('custom')
depends=('gtk3' 'gconf' 'nss' 'alsa-lib' 'libxss' 'libgnome-keyring' 'ttf-font')
optdepends=('cups: Printer support'
            'pepper-flash: Adobe Flash support')
provides=('brave-browser')
conflicts=("${pkgname}-latest" 'brave-bin' 'brave-beta-bin')
source=("$pkgname-$pkgver.zip::https://github.com/brave/brave-browser/releases/download/v${pkgver}/brave-v${pkgver}-linux-x64.zip"
        'MPL2::https://raw.githubusercontent.com/brave/browser-laptop/master/LICENSE.txt'
        "$pkgname.sh"
        "$pkgname.desktop"
        "braveAbout.png")
options=(!strip)
sha512sums=('ae3740657561b3d0a9dadcccfdb57136bcb60691fca54754c8f0c43314f9be25d96d12b326c409ce720ea62ba04ee5eea487b76ea7fe9a11699b567a439c7091'
            'b8823586fead21247c8208bd842fb5cd32d4cb3ca2a02339ce2baf2c9cb938dfcb8eb7b24c95225ae625cd0ee59fbbd8293393f3ed1a4b45d13ba3f9f62a791f'
            '1a767416f980e1767be6cefc13e18ac554cd0f015d7f06beb75d0335eb6847750bbf98030d1a1cb42f2460e5cfe7c58ce9a293a387245cff056fc1fb2f70f4fa'
            'd9b1e0bfc0759dfff35f8315acf695856401116d7b1a4f458a3d8c7aa0d75b963110341fe58fcd3b71a94c37b3f7a112cc1068bad594d67d81319e0ad34cfd8b'
            'd7bef52e336bd908d24bf3a084a1fc480831d27a3c80af4c31872465b6a0ce39bdf298e620ae9865526c974465807559cc75610b835e60b4358f65a8a8ff159e')
noextract=("$pkgname-$pkgver.zip")

prepare() {
  mkdir -p brave
  cat $pkgname-$pkgver.zip | bsdtar -xf- -C brave
  chmod +x brave/brave
}

_bsdtardir="brave"

package() {
    install -d -m0755 "$pkgdir/usr/lib"
    cp -a --reflink=auto $_bsdtardir "$pkgdir/usr/lib/$pkgname"

    install -Dm0755 "$pkgname.sh" "$pkgdir/usr/bin/brave-latest"
    install -Dm0644 -t "$pkgdir/usr/share/applications" "$pkgname.desktop"
    install -Dm0644 "braveAbout.png" "$pkgdir/usr/share/pixmaps/brave-latest.png"
    install -Dm0664 -t "$pkgdir/usr/share/licenses/$pkgname" "MPL2"
    mv "$pkgdir/usr/lib/$pkgname/"{LICENSE,LICENSES.chromium.html} "$pkgdir/usr/share/licenses/$pkgname"

    ln -s /usr/lib/PepperFlash "$pkgdir/usr/lib/pepperflashplugin-nonfree"
}
