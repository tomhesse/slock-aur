pkgname=slock-custom
_pkgname=slock
pkgver=1.4
pkgrel=2
pkgdesc="A simple X display locker"
url="https://tools.suckless.org/slock"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libxft' 'libxext' 'libxrandr')
provides=('slock')
conflicts=('slock')
source=(https://dl.suckless.org/tools/slock-$pkgver.tar.gz
        https://tools.suckless.org/slock/patches/dpms/slock-dpms-1.4.diff
        config.h)
sha256sums=('b53849dbc60109a987d7a49b8da197305c29307fd74c12dc18af0d3044392e6a'
            '12af3ae1522d2423fb55d462896e1392797fd4073006a30a99d1b679535dbadf'
            '937e48cb800100a896ffcf1bdca966ecb50df7d1ab0098265a7bf1f94cb8bca3')

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
