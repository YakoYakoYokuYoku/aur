# Maintainer: Oleg Shparber <trollixx+aur@gmail.com>
# Contributor: Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Andrea Scarpino <andrea@archlinux.org>
# Contributor: Sébastien Luttringer
# Contributor: xduugu
# Contributor: Ronald van Haren <ronald.archlinux.org>
# Contributor: Vesa Kaihlavirta
# URL: https://github.com/trollixx/aur-packages
# Upstream: https://projects.archlinux.org/svntogit/community.git/tree/trunk?h=packages/awesome

_pkgname=awesome
pkgname=${_pkgname}-git
pkgver=3.5.6
pkgrel=1
pkgdesc='Highly configurable framework window manager'
arch=('i686' 'x86_64')
url='http://awesome.naquadah.org/'
license=('GPL2')
depends=('cairo' 'dbus' 'gdk-pixbuf2' 'imlib2' 'libxdg-basedir' 'lua' 'lua-lgi'
         'pango' 'startup-notification' 'xcb-util-cursor' 'xcb-util-keysyms'
         'xcb-util-wm' 'xorg-xmessage')
makedepends=('asciidoc' 'cmake' 'docbook-xsl' 'doxygen' 'imagemagick' 'ldoc' 'xmlto')
optdepends=('rlwrap: readline support for awesome-client'
            'dex: autostart your desktop files'
            'vicious: widgets for the Awesome window manager')
provides=('notification-daemon')
backup=('etc/xdg/awesome/rc.lua')
source=("${pkgname}-${pkgver}::git://github.com/awesomeWM/awesome.git")
md5sums=('SKIP')

prepare() {
  mkdir -p build
}

build() {
  cd build
  cmake ../$pkgname-$pkgver \
    -DCMAKE_BUILD_TYPE=RELEASE \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DSYSCONFDIR=/etc \
    -DLUA_LIBRARY=/usr/lib/liblua.so.5.2
  make
}

package() {
  cd build
  make DESTDIR="$pkgdir" install

  install -Dm644 "$srcdir"/$pkgname-$pkgver/awesome.desktop \
    "$pkgdir/usr/share/xsessions/awesome.desktop"
}
