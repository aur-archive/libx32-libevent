# Upstream Maintainer: josephgbr <rafael.f.f1@gmail.com>
# Contributor: Judd <jvinet@zeroflux.org>
# Maintainer: Fantix King <fantix.king at gmail.com>

_pkgbase=libevent
pkgname=libx32-${_pkgbase}
pkgver=2.0.20
pkgrel=1.2
pkgdesc="An event notification library (x32 ABI)"
arch=('x86_64')
url="http://www.monkey.org/~provos/libevent/"
license=('GPL2')
depends=('libx32-openssl' "${_pkgbase}=${pkgver}")
makedepends=('gcc-multilib-x32')
options=('!libtool')
source=(
    https://github.com/downloads/${_pkgbase}/${_pkgbase}/${_pkgbase}-$pkgver-stable.tar.gz
    event-config-stub.h)
md5sums=('94270cdee32c0cd0aa9f4ee6ede27e8e'
         '5ce006234020f4e9dd31ae4cbe0335b7')

build() {
  export CC='gcc -mx32'
  export CXX='g++ -mx32'
  export PKG_CONFIG_PATH='/usr/libx32/pkgconfig'

  cd ${_pkgbase}-${pkgver}-stable
  ./configure --prefix=/usr --sysconfdir=/etc --libdir=/usr/libx32
  make
}

package() {
  install="${pkgname}.install"
  cd ${_pkgbase}-${pkgver}-stable
  make DESTDIR="${pkgdir}" install

  mv "${pkgdir}/usr/include/event2/event-config.h" "${srcdir}/event-config-x32.h"
  rm -rf "${pkgdir}"/usr/{bin,include}
  install -Dm644 "${srcdir}/event-config-x32.h" "${pkgdir}/usr/include/event2/event-config-x32.h"
  install -Dm644 "${srcdir}/event-config-stub.h" "${pkgdir}/usr/include/event2/event-config-stub.h"
}
