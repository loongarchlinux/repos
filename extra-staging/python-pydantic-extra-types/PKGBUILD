# Maintainer: David Runge <dvzrv@archlinux.org>

_name=pydantic-extra-types
pkgname=python-pydantic-extra-types
pkgver=2.0.0
pkgrel=1
pkgdesc="Extra pydantic types"
arch=(any)
url="https://github.com/pydantic/pydantic-extra-types"
license=(MIT)
depends=(
  python
  python-pydantic
  python-pydantic-core
)
makedepends=(
  python-build
  python-hatchling
  python-installer
)
checkdepends=(
  python-dirty-equals
  python-phonenumbers
  python-pycountry
  python-pytest
)
optdepends=(
  'python-phonenumbers: for phone number support'
  'python-pycountry: for country code support'
)
source=($_name-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz)
sha512sums=('dde02fcec13431ba342a9f945b3dcd35b3d80c3f779cb75fcba9abdca51734b25fd108aff566822b68f97430fb70e2567fb2d9153107b884371eccd2d4ce31de')
b2sums=('9551ea0e1c7338a7c6fd1b882e65d085ae8c3f746fda47eb46c4bafdd43d6bca75aeb21fda399907e266d82c8b46b9b63993dd79d6e20aa4a2c5e0b69501a35b')

build() {
  cd $_name-$pkgver
  python -m build --wheel --no-isolation
}

check() {
  cd $_name-$pkgver
  pytest -vv
}

package() {
  cd $_name-$pkgver
  python -m installer --destdir="$pkgdir" dist/*.whl
  install -vDm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname/"
  install -vDm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname/"
}
