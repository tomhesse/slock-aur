pkgname=slock-custom
_pkgname=slock
pkgver=1.4
pkgrel=1
pkgdesc="A simple X display locker"
url="https://tools.suckless.org/slock"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libxft' 'libxext' 'libxrandr')
provides=('slock')
conflicts=('slock')
source=(https://dl.suckless.org/tools/slock-$pkgver.tar.gz
        config.h)
sha256sums=('b53849dbc60109a987d7a49b8da197305c29307fd74c12dc18af0d3044392e6a'
            'f4c746c86d8933f187a6ca64c83b30c9b948f5d6f84139511dcf6f7d7322b0a6')

prepare() {
  cd "$srcdir/$_pkgname-$pkgver"
  cp "$srcdir/config.h" config.h

  for patch in "$srcdir"/*.diff; do
    if [ -f "$patch" ]; then
      echo "Applying $(basename "$patch")"
      patch -p1 --quiet < "$patch"
    fi
  done
}

build() {
  cd "$srcdir/$_pkgname-$pkgver"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd "$srcdir/$_pkgname-$pkgver"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$_pkgname/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/$_pkgname/README"
}
