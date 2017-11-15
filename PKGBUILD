# Maintainer: Devin J. Pohly <djpohly+arch@gmail.com>
# Contributor: sl1pkn07
# Contributor: Ryan Peters <sloshy45 at sbcglobal dot net>
# Contributor: Artefact2 <artefact2@gmail.com>
# Contributor: Lauri Niskanen <ape@ape3000.com>
# Contributor: Travis Nickles <ryoohki7@yahoo.com>
# Contributor: Stefan Lohmaier <noneuss at gmail dot com>
# Contributor: Dan Guzek <dguzek@gmail.com>
pkgname=etterna-git
_shortname=stepmania
pkgver=0.56.2+CalcOnly+0+gbb6dfc5cc1
pkgrel=1
pkgdesc="Advanced cross-platform rhythm game designed for home and arcade use"
arch=('i686' 'x86_64')
url="http://www.stepmania.com/"
license=('MIT')
depends=('gtk2' 'libmad' 'jack' 'libpulse' 'libva')
makedepends=('git' 'cmake' 'yasm' 'glew')
provides=('stepmania=5.1')
conflicts=('stepmania')
replaces=('sm-ssc-hg')
install="$_shortname.install"
source=("git+https://github.com/etternagame/etterna.git#branch=0.56.2-CalcOnly"
        "$_shortname.sh")
sha256sums=('SKIP'
            'f9839a0c751fee40a5c21712110bce9f3b73863ece404f1c7e468d0fc1b528eb')

pkgver() {
  cd "$srcdir/etterna"
  git describe --long --tags | sed -e 's/-/+/g' -e 's/^v//'
}

prepare() {
  cd "$srcdir/etterna"

  # Use local clones for submodules
  git submodule init
  git submodule update
}

build() {
  mkdir -p "$srcdir/etterna/Build"
  cd "$srcdir/etterna/Build"
  cmake ..
  make
}

package() {
  cd "$srcdir/etterna"

  # Install program
  install -d "$pkgdir/opt/$_shortname"/{RandomMovies,Packages}
  install -t "$pkgdir/opt/$_shortname/" stepmania GtkModule.so
  install -D "$srcdir/$_shortname.sh" "$pkgdir/usr/bin/$_shortname"

  # Install miscellaneous directories
  cp -r -t "$pkgdir/opt/$_shortname/" Announcers BGAnimations BackgroundEffects \
      BackgroundTransitions Characters Data Docs NoteSkins Scripts \
      Songs Themes

  # Install auxiliary files
  install -Dm644 stepmania.desktop "$pkgdir/usr/share/applications/stepmania.desktop"
  install -d "$pkgdir/usr/share"
  cp -r icons "$pkgdir/usr/share/icons"

  # Install license
  install -Dm644 "Docs/Licenses.txt" "$pkgdir/usr/share/licenses/$pkgname/Licenses.txt"
}

# vim:set ts=2 sw=2 et:
