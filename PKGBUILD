# See also the official package:
# https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/xterm
# Contributor: Frédéric Mangano <fmang+aur at mg0.fr>

pkgname=xterm-needle
_realname=xterm
pkgver=316
pkgrel=1
pkgdesc="xterm patched for automatic selection from keyboard"
arch=('i686' 'x86_64')
url="http://invisible-island.net/xterm/"
license=('custom')
depends=('libxft' 'libxaw' 'ncurses' 'xorg-luit' 'xbitmaps' 'libutempter' 'libxkbfile')
provides=("${_realname}")
conflicts=("${_realname}")
source=(ftp://invisible-island.net/${_realname}/${_realname}-${pkgver}.tgz{,.asc}
        LICENSE
        xterm-needle.patch)
md5sums=('cb70f35405c346cbb673f3269476f10a'
         'SKIP'
         '10ecc3f8ee91e3189863a172f68282d2'
         '2b244cdc32bca61327428efc1ec686dc')
validpgpkeys=('C52048C0C0748FEE227D47A2702353E0F7E48EDB') # "Thomas Dickey <dickey@invisible-island.net>"

prepare() {
  cd "${srcdir}/${_realname}-${pkgver}"
  patch -p1 -i "${srcdir}/xterm-needle.patch"
}

build() {
  cd "${srcdir}/${_realname}-${pkgver}"
  ./configure --prefix=/usr \
      --libdir=/etc \
      --mandir=/usr/share/man \
      --with-app-defaults=/usr/share/X11/app-defaults/ \
      --with-x \
      --disable-full-tgetent \
      --disable-imake \
      --enable-ansi-color \
      --enable-88-color \
      --enable-256-color \
      --enable-broken-osc \
      --enable-broken-st \
      --enable-load-vt-fonts \
      --enable-i18n \
      --enable-wide-chars \
      --enable-doublechars \
      --enable-warnings \
      --enable-tcap-query \
      --enable-logging \
      --enable-dabbrev \
      --enable-freetype \
      --enable-luit \
      --enable-mini-luit \
      --enable-narrowproto \
      --enable-exec-xterm \
      --with-tty-group=tty \
      --with-utempter
  make
}

package() {
  cd "${srcdir}/${_realname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
  chmod 0755 "${pkgdir}/usr/bin/xterm"

  install -m755 -d "${pkgdir}/usr/share/licenses/${_realname}"
  install -m644 "${srcdir}/LICENSE" \
      "${pkgdir}/usr/share/licenses/${_realname}/"
  install -m755 -d ${pkgdir}/usr/share/applications
  install -m644 ${srcdir}/${_realname}-${pkgver}/{xterm,uxterm}.desktop ${pkgdir}/usr/share/applications/
}
