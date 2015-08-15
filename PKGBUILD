# Maintainer: Jens Staal <staal1978@gmail.com>
# contributor: almehdi

pkgname=fribid
pkgver=1.0.4
pkgrel=2
pkgdesc="A Free re-implementation of the Swedish BankID/eID system"
arch=('i686' 'x86_64')
url="http://fribid.se/"
license=('custom')
depends=('gettext' 'glib2' 'gtk2' 'openssl' 'opensc' 'libp11' )
optdepends=('openct: smartcard support')
provides=('nexuspersonal')
conflicts=('nexuspersonal' 'fribid-git')
source=("http://fribid.se/releases/source/fribid-${pkgver}.tar.bz2")
md5sums=('253e1eee92bebd5b37e0a508bda770cb')
options=('!strip')

build() {
  cd  "$srcdir/${pkgname}-${pkgver}"
  ./configure --prefix=/usr --pkcs11-module=/usr/lib/pkcs11/opensc-pkcs11.so
  sed -i 's/-DGTK_DISABLE_DEPRECATED=1 -DGDK_DISABLE_DEPRECATED=1 -DG_DISABLE_DEPRECATED=1//' client/Makefile
  sed -i 's/strndup/strndup_/' plugin/pluginutil.c
  make
}

package() {
  cd  "$srcdir/${pkgname}-${pkgver}"
  make DESTDIR="$pkgdir/" install
  install -Dm644 "$srcdir/${pkgname}-${pkgver}/LICENSE" "$pkgdir/usr/share/licenses/fribid/LICENSE"
}