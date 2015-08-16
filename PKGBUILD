# Maintainer:  Yangtse Su<yangtsesu@gmail.com>
# Contributor:  Jekyll Wu<adaptee [at] gmail [dot] com>
# Contributor: riverscn<riverscn at gmail.com>
# Contributor: rainy<rainylau at gmail.com>
# Contributor: Lee.MaRS<leemars at gmail.com>

pkgname=ibus-libpinyin
pkgver=1.4.93
pkgrel=1
pkgdesc="Intelligent Pinyin engine based on libpinyin for IBus"
arch=('i686' 'x86_64')
license=('LGPL')
url="https://github.com/libpinyin"
depends=('ibus>=1.4' 'libsigc++2.0' 'python2' 'libpinyin')
makedepends=('git' 'intltool' 'gnome-common')
replace=('ibus-pinyin-libpinyin-git')
conflicts=('ibus-libpinyin-git' 'ibus-pinyin-libpinyin-git')
source=(https://github.com/downloads/libpinyin/ibus-libpinyin/${pkgname}-${pkgver}.tar.gz)
md5sums=("95f6143323deddaf6d82020dcc14a1af")

build() {
  cd ${srcdir}
  rm -rf "${srcdir}/${pkgname}-build"
  cp -r "${srcdir}/${pkgname}-${pkgver}" "${srcdir}/${pkgname}-build"
  cd "${srcdir}/${pkgname}-build"

  msg "Starting make..."
  cd "${srcdir}/${pkgname}-build"

  # python2 fix
  for file in $(find . -name '*.py' -print); do
    sed -i 's_^#!.*/usr/bin/python_#!/usr/bin/python2_' $file
    sed -i 's_^#!.*/usr/bin/env.*python_#!/usr/bin/env python2_' $file
  done

  for file in setup/ibus-setup-libpinyin.in; do
    sed -i 's_exec python_exec python2_' $file
  done

  ./autogen.sh --prefix=/usr
  make
}

package() {
  cd "${srcdir}/${pkgname}-build"
  make NO_INDEX=true DESTDIR=${pkgdir} install
}
