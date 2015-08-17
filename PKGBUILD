# Maintainer: speps <speps dot archlinux dot org>

pkgname=qxmledit
pkgver=0.8.11
pkgrel=1
pkgdesc="Simple Qt XML editor and XSD viewer"
arch=('i686' 'x86_64')
url="http://code.google.com/p/qxmledit/"
license=('GPL3' 'LGPL3')
depends=('qt5-svg' 'qt5-xmlpatterns' 'desktop-file-utils')
install="$pkgname.install"
source=("https://googledrive.com/host/0B4p7QlvKSOF1RXI4alN6dWxYa1k/qxmledit-$pkgver-src.tgz")
md5sums=('c1251b088b6d6813351ff99c0df5929d')

prepare() {
  cd $pkgname-$pkgver

  # fix desktop file
  sed -e '1i[Desktop Entry]' \
      -e '/Encoding/d;/#/d' \
      -i install_scripts/environment/desktop/QXmlEdit.desktop

  # dot not install to /opt
  sed -e "s|\(INST_DIR = /\).*|\1usr/bin|" \
      -e "s|\(INST_DATA_DIR = /\).*|\1usr/share/$pkgname|" \
      -e "s|\(INST_DOC_DIR = /\).*|\1usr/share/doc/$pkgname|" \
      -e "s|\(INST_INCLUDE_DIR = /\).*|\1usr/include/$pkgname|" \
      -e "s|\(INST_LIB_DIR = /\).*|\1usr/lib|" \
      -i `find . -name "*.pro"`
}

build() {
  cd $pkgname-$pkgver
  qmake
  make
}

package() {
  cd $pkgname-$pkgver
  make INSTALL_ROOT="$pkgdir/" install

  # desktop
  install -Dm644 install_scripts/environment/desktop/QXmlEdit.desktop \
    "$pkgdir/usr/share/applications/QXmlEdit.desktop"

  # icon
  install -Dm644 install_scripts/environment/icon/qxmledit_48x48.png \
    "$pkgdir/usr/share/pixmaps/$pkgname.png"
}
