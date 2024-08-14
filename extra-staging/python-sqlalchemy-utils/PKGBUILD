# Maintainer: Jelle van der Waa <jelle@archlinux.org
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Husam Bilal <husam212 AT gmail DOT com>

_name=sqlalchemy-utils
pkgname=python-sqlalchemy-utils
pkgver=0.42.2
pkgrel=1
pkgdesc='Various utility functions, new data types and helpers for SQLAlchemy'
url='https://github.com/kvesteri/sqlalchemy-utils'
depends=('python' 'python-sqlalchemy' 'python-anyjson' 'python-babel'
         'python-arrow' 'python-intervals' 'python-phonenumbers' 'python-passlib'
         'python-colour' 'python-dateutil' 'python-furl' 'python-cryptography'
         'python-pendulum')
checkdepends=('python-pytest' 'python-flexmock' 'python-jinja')
makedepends=('python' 'python-setuptools' 'python-build' 'python-installer' 'python-wheel')
license=('BSD')
arch=('any')
source=(https://github.com/kvesteri/sqlalchemy-utils/archive/${pkgver}/${pkgname}-${pkgver}.tar.gz)
sha512sums=('54b770cbde6a7131229bc1b5166dd476a4ba061e470b2eb9a7c23c085f80e413bafe11b3ea98d60906669c25cca19b35d4a068df59c7858b54f8e5d19ea61f3e')
b2sums=('65a59ab46b0dd54756b65bae1d9d120beeff6d0f142e1b6025cee6ae9152082615ed3eddd9356ab22033746f4984969d6b76ab46cf0fee80026c3a2067d69724')

build() {
  cd ${_name}-${pkgver}
  python -m build --wheel --no-isolation
}

check() {
  cd ${_name}-${pkgver}
  # Tests require a postgres and MySQL db
  export PYTHONWARNINGS="ignore"
  pytest -Wignore --disable-pytest-warnings tests/test_models.py
}

package() {
  cd ${_name}-${pkgver}
  python -m installer --destdir="${pkgdir}" dist/*.whl
  install -Dm 644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim: ts=2 sw=2 et:
