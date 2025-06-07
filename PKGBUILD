# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer:
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Maintainer:
#   Felix Yan
#     <felixonmars@archlinux.org>
# Contributor:
#   onny
#     <onny@project-insanity.org>

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
_pkg=passlib
pkgname="${_py}-${_pkg}"
pkgver=1.7.4
pkgrel=10
pkgdesc=(
  "A password hashing"
  "library for Python."
)
arch=(
  'any'
)
url="https://${_pkg}.readthedocs.io/en/stable"
license=(
  'custom:BSD'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  "${_py}-setuptools"
)
checkdepends=(
  "${_py}-nose"
  "${_py}-bcrypt"
  "${_py}-django"
  "${_py}-fastpbkdf2"
  "${_py}-scrypt"
)
_fastpbkdf2_optdepends=(
  "${_py}-fastpbkdf2:"
    "Accelerate PBKDF2-based hashes."
)
_bcrypt_optdepends=(
  "${_py}-bcrypt:"
    "Accelerate Bcrypt hashes."
)
_scrypt_optdepends=(
  "${_py}-scrypt:"
    "Accelerates SCrypt hashes."
)
optdepends=(
  "${_fastpbkdf2_optdepends[*]}"
  "${_bcrypt_optdepends[*]}"
  "${_scrypt_optdepends[*]}"
)
_pypa="https://pypi.io/packages/source"
_ns="${_pkg::0}"
_url="${_pypa}/${_ns}/${_pkg}"
_tarname="${_pkg}-${pkgver}"
source=(
  "${_pypa}/${_tarname}.tar.gz"
  "${_py}-passlib-bcrypt.patch"
)
sha512sums=(
  '350bd6da5ac57e6c266ffe8bf9684c8c2cce3fc6b513eb6c7bc1b302d2d8a1b701e9c01c953782520a2ac37b7ec1f6d7bd5855f99f6ee0e2dbbf33f2d49a9530'
  'c4c889f14485b75746f2424149b64bceb2a47fd40f3b847ed2ef4af5730ea5287d6fff61cdb805042f639f15f0cf70a54b0950912c19b87508dc8c0b267c1f5b'
)

prepare() {
  cd \
    "${srcdir}/${_tarname}"
  patch \
    -Np1 \
    -i \
    "../${pkgname}-bcrypt.patch"
}

check() {
  export \
    PASSLIB_TEST_MODE="full"
  cd \
    "${srcdir}/${_tarname}"
  "${_py}" \
    "setup.py" \
    nosetests || \
  echo \
    "https://bitbucket.org/ecollins/passlib/issues/98/${_pkg}extdjango-with-django-1112-fails"
}

package() {
  cd \
    "${_tarname}"
  "${_py}" \
    "setup.py" \
      install \
        -O1 \
        --root="${pkgdir}"
  install \
    -vDm644 \
    "LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

# vim:set ts=2 sw=2 et:
