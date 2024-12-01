# Maintainer: Hiroaki Yamamoto <hrak1529@gmail.com>

_pkgname=labwc
pkgname=labwc-im-git
pkgver=0.8.1.r108.g83c583c6
pkgrel=1
pkgdesc='stacking wayland compositor with look and feel from openbox (git version with minimal text-input-v1 support)'
url="https://github.com/labwc/labwc"
arch=('x86_64')
license=('GPL2')
depends=('libpng' 'librsvg' 'pango' 'libsfdo' 'seatd' 'libwlroots-0.18.so' 'wayland' 'xorg-xwayland')
makedepends=('git' 'meson' 'scdoc' 'wayland-protocols')
optdepends=("bemenu: default launcher via Alt+F3")
conflicts=(labwc)
provides=(labwc)
source=("git+https://github.com/labwc/${_pkgname}.git"
        '0001-IME-support-text-input-v1.patch'
        'fix-pixman-error.patch')
md5sums=('SKIP'
         '634e8a3d65ff9667be0f37402f7b26bc'
         '9aac6e8c564502b59a2a587332d78be3')

pkgver() {
  cd "$_pkgname"
  git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd "$_pkgname"
  patch -Np1 -i ../0001-IME-support-text-input-v1.patch
  patch -Np1 -i ../fix-pixman-error.patch
}

build() {
  arch-meson -Dman-pages=enabled "$_pkgname" build
  meson compile -C build
}

package() {
  meson install -C build --destdir "$pkgdir"
}
