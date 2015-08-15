# $Id: PKGBUILD 79610 2010-05-04 20:23:20Z ibiru $
# Maintainer: Jan de Groot <jgc@archlinux.org>
# this package is compiled for cleartype Tillman Coghill a.k.a Liberion
#liberion@gmail.com
pkgname=gtk2-cleartype 
pkgver=2.20.1
pkgrel=2
pkgdesc="The GTK+ Toolkit (v2) compiled against cleartype"
arch=('i686' 'x86_64')
url="http://www.gtk.org/"
install=gtk2.install
depends=('libxft-cleartype' 'cairo-cleartype' 'freetype2-cleartype')
makedepends=( 'libxft-cleartype' 'cairo-cleartype' 'freetype2-cleartype' 'pkgconfig' 'gtk-doc' 'gobject-introspection')
replaces=('gtkprint-cups' 'gail')
conflicts=('gtkprint-cups' 'gail')
provides=('gail=1.22.3')
options=('!libtool' '!docs')
backup=(etc/gtk-2.0/gtkrc)
license=('LGPL')
source=(http://ftp.gnome.org/pub/gnome/sources/gtk+/2.20/gtk+-${pkgver}.tar.bz2
        xid-collision-debug.patch
	revert_64bit_fix.patch)
sha256sums=('0e081731d21e34ff45c82199490c2889504fa8b3c7e117c043e82ababaec0f65'
            'd758bb93e59df15a4ea7732cf984d1c3c19dff67c94b957575efea132b8fe558'
	    '20f3a03760f765b68b85b614810e5df4a689b609da1ae200aa30072475121b4c')

build() {
  cd "${srcdir}/gtk+-${pkgver}"
  patch -Np1 -i "${srcdir}/xid-collision-debug.patch" || return 1
  patch -RNp1 -i ${srcdir}/revert_64bit_fix.patch || retun 1

  CXX=/bin/false ./configure --prefix=/usr --sysconfdir=/etc \
      --localstatedir=/var --with-xinput=yes \
      --without-libjasper \
      --with-included-loaders=png || return 1
  make || return 1
  make DESTDIR="${pkgdir}" install || return 1

  echo 'gtk-fallback-icon-theme = "gnome"' > "${pkgdir}/etc/gtk-2.0/gtkrc" || return 1
}
