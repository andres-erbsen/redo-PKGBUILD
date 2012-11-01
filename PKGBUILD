# Maintainer: Your Name <youremail@domain.com>
pkgname=redo-python-git
pkgver=20121101
pkgrel=1
pkgdesc="Python implementation of the minimalistic redo build system"
arch=('any')
url="https://github.com/apenwarr/redo"
license=('GPL')
groups=()
depends=()
makedepends=('git python')
provides=('redo' 'redo-python')
conflicts=('redo' 'redo-python' 'redo-python2')
replaces=()
backup=()
options=()
install=
noextract=()
source=('py3.patch')
md5sums=('f19d98ea855aeeea4cc1aea1b8c44de3')


_gitroot=https://github.com/apenwarr/redo.git
_gitname=redo

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  patch -i "$srcdir/py3.patch"

  ./minimal/do # partial bash implementation of redo itself
}

package() {
  cd "$srcdir/$_gitname-build"
  DESTDIR="$pkgdir" ./minimal/do install
}

# vim:set ts=2 sw=2 et:
