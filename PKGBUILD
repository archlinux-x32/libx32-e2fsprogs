# $Id: PKGBUILD 79194 2012-10-31 11:05:34Z lcarlier $
# Maintainer:  Ionut Biru <ibiru@archlinux.org>
# Contributor: mightyjaym <jm.ambrosino@free.fr>
# Contributor: Mikko Seppälä <t-r-a-y@mbnet.fi>

_pkgbasename=e2fsprogs
pkgname=lib32-e2fsprogs
pkgver=1.42.6
pkgrel=1
pkgdesc="Ext2 filesystem libraries (32-bit)"
arch=('x86_64')
license=('GPL' 'LGPL' 'MIT')
url="http://e2fsprogs.sourceforge.net"
depends=('lib32-util-linux' $_pkgbasename)
makedepends=('bc' 'gcc-multilib')
source=("http://downloads.sourceforge.net/sourceforge/${_pkgbasename}/${_pkgbasename}-${pkgver}.tar.gz")
sha1sums=('cd05cd4205a00d01a6da821660cff386788e9be3')

build() {
  export CC="gcc -m32"
  export CXX="g++ -m32"
  export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"

  cd "${srcdir}/${_pkgbasename}-${pkgver}"
  ./configure --prefix=/usr --libdir=/usr/lib32 --with-root-prefix="" --enable-elf-shlibs \
      --disable-{debugfs,imager,resizer,fsck,uuidd,libuuid,libblkid}
  make
}

package() {
  cd "${srcdir}/${_pkgbasename}-${pkgver}"
  make DESTDIR="${pkgdir}" install-libs

  rm -rf "${pkgdir}"/usr/{bin,include,share}
  mkdir -p "$pkgdir/usr/share/licenses"
  ln -s $_pkgbasename "$pkgdir/usr/share/licenses/$pkgname"
}
