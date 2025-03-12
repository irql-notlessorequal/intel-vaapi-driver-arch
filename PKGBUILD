# Maintainer: irq-notlessoreq <itistotalbotnet+aur AT SIGN gmail DOT com>

pkgname=libva-intel-driver-irql
pkgver=2.4.3
pkgrel=1
pkgdesc='VA-API implementation for Intel G45 and HD Graphics family (IRQL fork)'
arch=(x86_64)
url=https://github.com/irql-notlessorequal/intel-vaapi-driver
license=(MIT)
depends=(
  libva
  libdrm
)
makedepends=(
  git
  meson
)
replaces=(libva-driver-intel libva-intel-driver)
conflicts=(libva-intel-driver)
provides=(libva-intel-driver)
source=(git+https://github.com/irql-notlessorequal/intel-vaapi-driver.git#tag=6d64cf2904672d618f0b8fcce13e95a120e1a5aa)
sha256sums=('SKIP')

pkgver() {
  cd intel-vaapi-driver

  git describe --tags
}

prepare() {
  cd intel-vaapi-driver

  # Only relevant if intel-gpu-tools is installed,
  # since then the shaders will be recompiled
  sed -i '1s/python$/&2/' src/shaders/gpp.py
}

build() {
  CFLAGS+=' -fcommon' # https://wiki.gentoo.org/wiki/Gcc_10_porting_notes/fno_common
  arch-meson intel-vaapi-driver build
  ninja -C build
}

package() {
  DESTDIR="${pkgdir}" meson install -C build

  # My fork renamed the COPYING file into LICENSE.
  install -Dm644 intel-vaapi-driver/LICENSE -t "${pkgdir}"/usr/share/licenses/$pkgname
}

# vim: ts=2 sw=2 et:
