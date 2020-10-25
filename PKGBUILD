# Maintainer: Philip Müller <philm@manjaro.org>
# Contributor: Caleb Maclennan <caleb@alerque.com>
# Contributor: Jacob Mischka <jacob@mischka.me>
# Contributor: Manuel Mazzuola <origin.of@gmail.com>

pkgname=brave-beta
pkgver=1.17.46
pkgrel=1
pkgdesc='Web browser that blocks ads and trackers by default (latest binary release).'
arch=('x86_64')
url='https://github.com/brave/brave-browser/releases'
license=("MPL2" "BSD" "custom:chromium")
depends=("gtk3" "nss" "alsa-lib" "libxss" "ttf-font")
optdepends=("cups: Printer support"
            "pepper-flash: Adobe Flash support"
            "libgnome-keyring: Enable GNOME keyring support")
provides=("${pkgname%-bin}" "brave-browser" "brave")
conflicts=("${pkgname%-bin}" "brave")
source=("${pkgname}-${pkgver}.zip::https://github.com/brave/brave-browser/releases/download/v${pkgver}/brave-browser-beta-${pkgver}-linux-amd64.zip"
        "LICENSE::https://raw.githubusercontent.com/brave/brave-browser/master/LICENSE"
        "$pkgname.sh"
        "brave-browser.desktop"
        "logo.png")
options=(!strip)
sha512sums=('2eed2119179cc684160889dd64cebb261817f10e621845000ff969779c643db1ea07fb4990ad14b4374f4bd9cbe44c7cc2b877503341a43e14bc916e7d6c9644'
            '239dbc27d68e0a03e92c68fb746602d8183084c9624a533fe92a991b8a4658d5154c901ff64826992eabcf89a5b52cb32f9cf29fd25a42bef2b5d3932010d806'
            'f29f4836b113d08c46b2e9cb67ed07e7c9660feabca579b2febeae69a9b7d12da6f14bf290ed73963d3f983b58f76000ef2930224704aeb64bce9da3907e054f'
            'c21aecaafec43bc1ce1ea3439667efb4c7ea5e54bfa87346a9ae9650de1e90c80174b1610a9216f936f693593816c9585c6be1875b3bd318d067079c06251e92'
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

    install -Dm0755 "$pkgname.sh" "$pkgdir/usr/bin/brave"
    install -Dm0644 -t "$pkgdir/usr/share/applications" "brave-browser.desktop"
    install -Dm0644 "logo.png" "$pkgdir/usr/share/pixmaps/brave.png"
    install -Dm0664 -t "${pkgdir}/usr/share/licenses/${pkgname}" "LICENSE"
    ln -s /usr/lib/PepperFlash "${pkgdir}/usr/lib/pepperflashplugin-nonfree"
}
