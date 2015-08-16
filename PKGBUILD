# Maintainer: spider-mario <spidermario@free.fr>
# Contributor: helq
pkgname=laby
pkgver=0.6.4
pkgrel=1
pkgdesc="Small program to learn how to program with ants and spider webs"
arch=('i686' 'x86_64')
url="https://github.com/sgimenez/laby"
license=('GPL3')
depends=('gtksourceview2')
makedepends=('ocaml-findlib' 'lablgtk2' 'imagemagick')
source=($pkgname-$pkgver.tar.gz::https://github.com/sgimenez/$pkgname/tarball/$pkgname-$pkgver
        laby.6.gz
        laby.desktop
        laby.svg)
md5sums=('0aa2e4ad2cc8aeb9bc9de2b42984457a'
         '06d288577fcf8998b640d01fb6d3a53e'
         'b179245490c7dacc5eba83d3d267efcc'
         '9ac122ca0b2446ecdea729417db9f9df')

_dirname=sgimenez-laby-e6d7834

has() {
  [ -x "$(which "$1")" ]
}

build() {
  cd "$_dirname"

  ./build

  pushd data/tiles
    for f in *.svg
    do
      p="${f/%svg/png}"
      convert "$f" "$p"
      if has optipng; then optipng -o7 "$p"; fi
      if has advpng; then advpng -z -4 "$p"; fi
    done
  popd
}

package() {
  cd "$_dirname"

  install --directory "$pkgdir"/usr/bin
  install laby "$pkgdir"/usr/bin/

  install --directory "$pkgdir"/usr/share/applications
  cp "$srcdir/laby.desktop" "$pkgdir"/usr/share/applications/

  install --directory "$pkgdir"/usr/share/icons/hicolor/scalable/apps
  install --directory "$pkgdir"/usr/share/pixmaps
  cp "$srcdir/laby.svg" "$pkgdir"/usr/share/icons/hicolor/scalable/apps/
  pushd "$pkgdir"/usr/share/pixmaps
    ln --symbolic ../icons/hicolor/scalable/apps/laby.svg laby.svg
  popd

  install --directory "$pkgdir"/usr/share/man/man6
  cp "$srcdir/laby.6.gz" "$pkgdir"/usr/share/man/man6/

  install --directory "$pkgdir"/usr/share
  cp --recursive data "$pkgdir"/usr/share/laby
}

# vim:set ts=2 sw=2 et:
