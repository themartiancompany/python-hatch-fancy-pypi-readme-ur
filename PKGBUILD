# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg="hatch-fancy-pypi-readme"
pkgname="${_py}-${_pkg}"
pkgver=23.1.0
pkgrel=1
pkgdesc='Fancy PyPI READMEs with Hatch'
arch=(
  any
)
_http="https://github.com"
_ns="hynek"
url="${_http}/${_ns}/${_pkg}"
license=(
  MIT
)
depends=(
  "${_py}-hatchling"
)
makedepends=(
  "${_py}-build"
  "${_py}-installer"
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-wheel"
)
source=(
  "${url}/archive/${pkgver}/${pkgname}-${pkgver}.tar.gz"
)
sha256sums=(
  '735b096c20d8b2ece32d9ab8e695cbfccb54d704770afb8f67f90a9236503811'
)

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  PYTHONPATH="$PWD"/src \
  pytest \
    -v
}

package() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -Dm644 \
    LICENSE.txt \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
