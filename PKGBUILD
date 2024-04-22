# Maintainer: Hiroaki Yamamoto <hrak1529@gmail.com>

_pkgname=labwc
pkgname=labwc-im-git
pkgver=0.7.1.r132.ga109e6e3
pkgrel=1
pkgdesc='stacking wayland compositor with look and feel from openbox (git version with minimal text-input-v1 support)'
url="https://github.com/labwc/labwc"
arch=('x86_64')
license=('GPL2')
depends=('libpng' 'librsvg' 'pango' 'seatd' 'wlroots>=0.17' 'wlroots<0.18' 'wayland' 'xorg-xwayland')
makedepends=('git' 'meson' 'scdoc' 'wayland-protocols')
optdepends=("bemenu: default launcher via Alt+F3")
conflicts=(labwc)
provides=(labwc)
source=("git+https://github.com/labwc/${_pkgname}.git"
        '0001-IME-support-text-input-v1.patch')
md5sums=('SKIP'
         'f87290362a7719025c745161266e7566')

pkgver() {
  cd "$_pkgname"
  git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd "$_pkgname"
  patch -Np1 -i ../0001-IME-support-text-input-v1.patch
}

build() {
  arch-meson -Dman-pages=enabled "$_pkgname" build
  meson compile -C build
}

package() {
  meson install -C build --destdir "$pkgdir"
}
