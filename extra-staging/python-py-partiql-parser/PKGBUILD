# Maintainer: Chih-Hsuan Yen <yan12125@archlinux.org>

pkgname=python-py-partiql-parser
_pkgname=py-partiql-parser
# https://github.com/getmoto/py-partiql-parser/blob/main/CHANGELOG.md
pkgver=0.5.4
pkgrel=1
pkgdesc='Python Parser for PartiQL'
arch=(any)
url='https://github.com/getmoto/py-partiql-parser'
# Most files are licensed under MIT, while an Apache 2.0 file is vendored since 0.4.0.
# See: https://github.com/getmoto/py-partiql-parser/pull/12
license=('MIT AND Apache-2.0')
depends=(python)
makedepends=(python-build python-installer python-hatchling)
checkdepends=(python-pytest)
source=("https://github.com/getmoto/py-partiql-parser/archive/refs/tags/$pkgver/$pkgname-$pkgver.tar.gz")
sha256sums=('f3c94d4de4c99604c3732298af0e1671ce8e2868866d40905b2bbb472b6f2b1d')

build() {
  cd $_pkgname-$pkgver

  python -m build --wheel --no-isolation
}

check() {
  cd $_pkgname-$pkgver

  pytest tests
}

package() {
  cd $_pkgname-$pkgver

  python -m installer --destdir="$pkgdir" dist/*.whl
  install -Dm644 LICENSE -t "$pkgdir"/usr/share/licenses/$pkgname
}
