# Maintainer: Fabian Bornschein <fabiscafe-at-mailbox-dot-org>
# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Contributor: Ionut Biru <ibiru@archlinux.org>

pkgname=gnome-user-docs
pkgver=45.0
pkgrel=1
pkgdesc="User documentation for GNOME"
url="https://gitlab.gnome.org/GNOME/gnome-user-docs"
arch=(any)
license=(FDL)
depends=(yelp)
makedepends=(
  git
  yelp-tools
)
groups=(gnome)
_commit=212a046dfa72da0c9aa8b200264e40b0aaf421fa  # tags/45.0^0
source=("git+https://gitlab.gnome.org/GNOME/gnome-user-docs.git#commit=$_commit")
b2sums=('SKIP')

pkgver() {
  cd $pkgname
  git describe --tags | sed 's/[^-]*-g/r&/;s/-/+/g'
}

prepare() {
  cd $pkgname
  NOCONFIGURE=1 ./autogen.sh
}

build() {
  local configure_options=(
    --prefix=/usr
    --sysconfdir=/etc
    --localstatedir=/var
  )

  cd $pkgname
  ./configure "${configure_options[@]}"
  make
}

package() {
  cd $pkgname
  make DESTDIR="$pkgdir" install
}

# vim:set sw=2 sts=-1 et:
