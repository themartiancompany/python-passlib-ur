# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: onny <onny@project-insanity.org>

pkgbase=python-passlib
pkgname=(python-passlib python2-passlib)
pkgver=1.7.0
pkgrel=2
pkgdesc="A password hashing library for Python"
arch=('any')
url="https://code.google.com/p/passlib/"
license=('custom:BSD')
makedepends=('python-setuptools' 'python2-setuptools')
checkdepends=('python-nose' 'python2-nose' 'python-bcrypt' 'python2-bcrypt'
              'python-django' 'python2-django' 'python2-m2crypto')
source=("https://pypi.io/packages/source/p/passlib/passlib-$pkgver.tar.gz")
sha512sums=('7187c4e5145e66be58e69f3f764d318e38e4d494c89020a441defb680d035fe3d96b5ad2f9f981ce5da91cf38e6ee444cbd752d5412b97c91abafac0ae393d6b')

prepare() {
  cp -a passlib-$pkgver{,-py2}
}

check() {
  export PASSLIB_TEST_MODE=full

  cd "$srcdir"/passlib-$pkgver
  python setup.py nosetests

  cd "$srcdir"/passlib-$pkgver-py2
  python2 setup.py nosetests
}

package_python-passlib() {
  depends=("python")
  optdepends=("python-bcrypt: accelerate Bcrypt hashes")

  cd passlib-$pkgver
  python setup.py install -O1 --root="$pkgdir"
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

package_python2-passlib() {
  depends=("python2")
  optdepends=("python2-m2crypto: accelerate PBKDF2-based hashes"
              "python2-bcrypt: accelerate Bcrypt hashes")

  cd passlib-$pkgver-py2
  python2 setup.py install -O1 --root="$pkgdir"
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

# vim:set ts=2 sw=2 et:
