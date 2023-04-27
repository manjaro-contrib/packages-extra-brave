# Maintainer: Stefano Capitani <stefano[at]manjaro[dot]org>

# Arch credits:
# Maintainer: Greg White <gwhite@kupulau.com>

_pkgname=brave
pkgname=$_pkgname-browser-beta
pkgver=1.52.78
pkgrel=1
pkgdesc='Web browser that blocks ads and trackers by default (beta binary release).'
arch=('x86_64')
url='https://brave.com/download-beta'
license=('MPL2')
depends=('gtk3' 'nss' 'alsa-lib' 'libxss' 'ttf-font')
optdepends=('cups: Printer support'
            'pepper-flash: Adobe Flash support'
            'mesa: Hardware accelerated rendering'
            'libglvnd: Support multiple different OpenGL drivers at any given time'
	    'libgnome-keyring: gnome keyriung support')
provides=('brave-beta-browser')
conflicts=('brave-beta-bin')
source=("https://github.com/brave/brave-browser/releases/download/v${pkgver}/brave-browser-beta_${pkgver}_amd64.deb"
        'MPL2::https://raw.githubusercontent.com/brave/browser-laptop/master/LICENSE.txt'
        brave-beta.sh)
options=(!strip)
sha512sums=('5d9bc65958f8806c2f1ee9de976a3f8773dc264c97401f6e3a3cbb8713e9e585b3b305db8a71a1ef7ea16ec20d176898518eab7db5e05776c75313eac88d4a5a'
            'b8823586fead21247c8208bd842fb5cd32d4cb3ca2a02339ce2baf2c9cb938dfcb8eb7b24c95225ae625cd0ee59fbbd8293393f3ed1a4b45d13ba3f9f62a791f'
            'b4aa6d6faf2b879d14310141dd92dc7144ff5b45a1075ee54451427029a01812a25f8249540d6bc9f0e9bbe6efc4d8913cc90d4c9546566b19fd1f605cf1a883')

prepare() {
  mkdir -p brave
  tar xf data.tar.xz -C brave
  # Delete unneeded cron job
  rm -rf brave/opt/brave.com/brave-beta/cron
  # Use our script to launch (allows overriding flags, sets up data dir)
  sed -i "s/\/usr\/bin\/brave-browser-beta/\/usr\/bin\/brave-beta/g" brave/usr/share/applications/brave-browser-beta.desktop    
}

package() {
    cp -a --reflink=auto brave/opt "$pkgdir/opt"
    cp -a --reflink=auto brave/usr "$pkgdir/usr"
    
    install -Dm0755 'brave-beta.sh' "$pkgdir/usr/bin/brave-beta"
    install -Dm0644 "brave/opt/brave.com/brave-beta/product_logo_128_beta.png" "$pkgdir/usr/share/pixmaps/brave-browser-beta.png"

    install -Dm0664 -t "$pkgdir/usr/share/licenses/$pkgname" "brave/opt/brave.com/brave-beta/LICENSE"
    chmod 4755 "$pkgdir/opt/brave.com/brave-beta/chrome-sandbox"
}
