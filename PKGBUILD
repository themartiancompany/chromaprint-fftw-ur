# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Daniel Bermond <dbermond@archlinux.org>

_pkg="chromaprint"
_backend="fftw"
_pkgname="${_pkg}-${_backend}"
pkgname="${_pkgname}"
pkgver=1.5.1
pkgrel=2
_pkgdesc=(
  "Library for extracting fingerprints from"
  "any audio source (uses fftw for FFT"
  "calculations instead of ffmpeg)"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'x86_64'
  'arm'
  'aarch64'
  'armv7l'
  'armv6l'
  'mips'
  'powerpc'
)
_author="acoustid"
url="https://${_author}.org/${_pkg}"
license=(
  'GPL'
)
depends=(
  "${_backend}"
)
makedepends=(
  'cmake'
  'gtest'
)
provides=(
  "${_pkg}"
  "lib${_pkg}.so"
)
conflicts=(
  "${_pkg}"
)
_gh="https://github.com"
_http="${_gh}"
_ns="${_author}"
_url="${_http}/${_ns}/${_pkg}"
source=(
  "${_url}/archive/v${pkgver}/${_pkg}-${pkgver}.tar.gz" 
  "010-${_pkg}-gtest-1.13.0-fix.patch"
)
sha256sums=(
  'a1aad8fa3b8b18b78d3755b3767faff9abb67242e01b478ec9a64e190f335e1c'
  '46e389235dd08c727d6cc1ae079a77d06fde337f4a06d0c0fe908d2025280f63'
)

prepare() {
  patch \
    -Np1 \
    -d \
      "${_pkg}-${pkgver}" \
    -i \
    "${srcdir}/010-${_pkg}-gtest-1.13.0-fix.patch"
}

build() {
  local \
    _cmake_opts=()
  _cmake_opts=(
    -DCMAKE_BUILD_TYPE:STRING='None'
    -DCMAKE_INSTALL_PREFIX:PATH='/usr'
    -DBUILD_TESTS:BOOL='ON'
    -DBUILD_TOOLS:BOOL='OFF'
    -DFFT_LIB:STRING='fftw3'
    -DGTEST_SOURCE_DIR:PATH='/usr/src/googletest'
    -Wno-dev
  )
  cmake \
    -B \
      build \
    -S \
      "${_pkg}-${pkgver}" \
    "${_cmake_opts[@]}"
  make \
    -C \
      build
}

check() {
  make \
    -C \
      build \
    check
}

package() {
  make \
    -C \
      build \
    DESTDIR="${pkgdir}" \
    install
}

