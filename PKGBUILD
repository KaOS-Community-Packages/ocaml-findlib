pkgname=ocaml-findlib
pkgver=1.5.5
pkgrel=1
license=('MIT')
arch=('x86_64')
pkgdesc='Objective Caml (OCaml) package manager'
url='http://projects.camlcity.org/projects/findlib.html'
depends=('ocaml')
source=("http://download.camlcity.org/download/findlib-$pkgver.tar.gz")
md5sums=('703eae112f9e912507c3a2f8d8c48498')
options=('staticlibs' '!strip' 'zipman' '!makeflags') # otherwise the bytecode gets broken

build() {
  cd "$srcdir/findlib-$pkgver"

  ./configure -config /etc/findlib.conf -sitelib /usr/lib/ocaml -mandir /usr/share/man
  make all opt
}

package () {
  cd "$srcdir/findlib-$pkgver"

  make prefix="$pkgdir" install 

  # add the old site-lib to the path to maintain compatibility with old style packages
  sed -i 's/path=\"\/usr\/lib\/ocaml\"/path="\/usr\/lib\/ocaml:\/usr\/lib\/ocaml\/site-lib"/' \
    "${pkgdir}/etc/findlib.conf"

  install -m755 src/findlib/ocamlfind_opt "$pkgdir/usr/bin/"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}