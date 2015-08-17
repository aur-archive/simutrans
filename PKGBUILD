# Maintainer: Balló György <ballogyor+arch at gmail dot com>
# Contributor: Anton Bazhenov <anton.bazhenov at gmail>
# Contributor: Jaroslav Lichtblau <dragonlord@aur.archlinux.org>
# Contributor: Gilles Gagniard <gilles@gagniard.org>
# Contributor: JD Steffen <jd at steffennet dot org>

pkgname=simutrans
pkgver=111.3
_pkgver=111-3
pkgrel=1
pkgdesc="An open source transportation simulation game"
arch=('i686' 'x86_64')
url="http://simutrans.com/"
license=('custom:Artistic License')
depends=('gcc-libs' 'zlib' 'sdl_mixer' 'simutrans-pak64>=110.0.1')
makedepends=('imagemagick')
source=(http://downloads.sourceforge.net/$pkgname/$pkgname-src-$_pkgver.zip
        http://downloads.sourceforge.net/$pkgname/simulinux-$_pkgver.zip
        settings-folder.patch
        path-for-game-data.patch
        config.patch
	fix-build.patch
        simutrans.desktop)
md5sums=('ae98217ffbd280556e2d5c9f9de11e10'
         '41b119178dd57898959f11d00768f2f3'
         'c87d9a9910bc371df5d50f7f1ec298bb'
         '4648680290b44775b9c47d3758d3bd6c'
         'd11bc8ee33a34e33341f6ccd90a44dba'
         '7d6329f7db821e3cc22fde5c5c138e2d'
         'f41f7a08ad517ef2b60412859eb49963')

build() {
  cd "$srcdir"

  cp config.template config.default
  patch -Np0 -i "$srcdir/settings-folder.patch"
  patch -Np1 -i "$srcdir/path-for-game-data.patch"
  patch -Np0 -i "$srcdir/config.patch"
  patch -Np0 -i "$srcdir/fix-build.patch"
  convert simutrans.ico -alpha on simutrans.png
  chmod 644 simsys_opengl.cc

  make
}

package() {
  cd "$srcdir"

  #binary
  install -Dm755 build/default/sim "$pkgdir/usr/bin/simutrans"

  #data
  mkdir -p "$pkgdir/usr/share/games/$pkgname"
  cp -r "$pkgname"/{config,font,music,skin,text} "$pkgdir/usr/share/games/$pkgname"

  #desktop file and icon
  install -Dm644 simutrans.png "$pkgdir/usr/share/pixmaps/simutrans.png"
  install -Dm644 simutrans.desktop "$pkgdir/usr/share/applications/simutrans.desktop"

  #license
  install -Dm644 "$pkgname"/license.txt "$pkgdir/usr/share/licenses/$pkgname/license.txt"
}
