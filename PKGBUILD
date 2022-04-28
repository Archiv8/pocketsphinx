#!/bin/bash

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# [Query]: Latest release was, 5prealpha on 2016/09/24 and latest repository update was 2018/02/10. Is pocketsphinx project abandoned?
# [ToDo]:  Add files: User documentation
# [ToDo]:  Add files: Tooling
# [FixMe]: Dependency, sphinxbase, fails to build
# [FixMe]: Namcap warnings and errors

# Maintainer: Ross Clark <archiv8@artisteducator.com>
# Contributor: Ross Clark <archiv8@artisteducator.com>

pkgname=pocketsphinx
pkgver=5prealpha
pkgrel=12
pkgdesc="Lightweight speech recognition engine"
arch=("i686" "x86_64")
url="http://cmusphinx.sourceforge.net"
license=("BSD")
makedepends=(
  # Arch Linux dependencies
  "swig"
  "python"
)
depends=(
  # Arch Linux dependencies
  "sphinxbase=5prealpha"
  "gst-plugins-base-libs"
)
source=(
  "http://downloads.sourceforge.net/cmusphinx/$pkgname-$pkgver.tar.gz"
)
sha512sums=(
  "ef5bb5547e2712bdf571f256490ef42a47962033892efd9d7df8eed7fe573ed9"
)
options=(
  "!libtool"
)

prepare() {
  cd "$pkgname-$pkgver"

  msg2 "Reconfiguring project for current version of Automake"
  autoreconf -ivf >/dev/null
}

build() {
  cd "$pkgname-$pkgver"

  export PYTHON=/usr/bin/python
  ./configure --prefix=/usr
  make
}

package() {
  cd "$pkgname-$pkgver"

  make DESTDIR="$pkgdir" install

  install -d -m755 "${pkgdir}/usr/share/licenses/${pkgname}"
  install -D -m644 "${srcdir}/${pkgname}-${pkgver}/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
