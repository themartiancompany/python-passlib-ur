# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: onny <onny@project-insanity.org>

pkgbase=python-passlib
pkgname=(python-passlib python2-passlib)
pkgver=1.7.1
pkgrel=2
pkgdesc="A password hashing library for Python"
arch=('any')
url="https://code.google.com/p/passlib/"
license=('custom:BSD')
makedepends=('python-setuptools' 'python2-setuptools')
checkdepends=('python-nose' 'python2-nose' 'python-bcrypt' 'python2-bcrypt' 'python-django'
              'python2-django' 'python2-m2crypto' 'python-fastpbkdf2' 'python2-fastpbkdf2'
              'python-scrypt' 'python2-scrypt')
source=("https://pypi.io/packages/source/p/passlib/passlib-$pkgver.tar.gz")
sha512sums=('3d5f069cd4e44e5e87cdabc46845acbdd6c1eeedb7ce1f611aebee87b0f7af19009b6a47a10ec555fd84260b9f5c933c6429e325d30326de3869f05031674168')

prepare() {
  cp -a passlib-$pkgver{,-py2}
}

check() {
  export PASSLIB_TEST_MODE=full

  cd "$srcdir"/passlib-$pkgver
  python setup.py nosetests || warning "https://bitbucket.org/ecollins/passlib/issues/98/passlibextdjango-with-django-1112-fails"

  cd "$srcdir"/passlib-$pkgver-py2
  python2 setup.py nosetests || warning "https://bitbucket.org/ecollins/passlib/issues/98/passlibextdjango-with-django-1112-fails"
}

package_python-passlib() {
  depends=("python")
  optdepends=("python-fastpbkdf2: accelerate PBKDF2-based hashes"
              "python-bcrypt: accelerate Bcrypt hashes"
              "python-scrypt: accelerate SCrypt hashes")

  cd passlib-$pkgver
  python setup.py install -O1 --root="$pkgdir"
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

package_python2-passlib() {
  depends=("python2")
  optdepends=("python2-fastpbkdf2: accelerate PBKDF2-based hashes"
              "python2-bcrypt: accelerate Bcrypt hashes"
              "python2-scrypt: accelerate SCrypt hashes")

  cd passlib-$pkgver-py2
  python2 setup.py install -O1 --root="$pkgdir"
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

# vim:set ts=2 sw=2 et:
