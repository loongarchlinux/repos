# Maintainer: David Runge <dvzrv@archlinux.org>

_name=nethsm-sdk-py
pkgname=python-nethsm-sdk-py
pkgver=0.5.0
pkgrel=1
pkgdesc="Client-side Python SDK for NetHSM"
arch=(any)
url="https://github.com/Nitrokey/nethsm-sdk-py"
license=(Apache-2.0)
depends=(
  python
  python-certifi
  python-cryptography
  python-dateutil
  python-typing-extensions
  python-urllib3
)
makedepends=(
  python-build
  python-flit-core
  python-installer
  python-wheel
)
provides=(python-nethsm)
source=($_name-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz)
sha512sums=('4b9c43ceaac8c1f4f0180fa0c0ecd1d8bab5b1eda6f17e550617fe01d5d88ed2cc183595399bdb9f00911d81ddda8966699c644479022893a6fb51271fa0ebee')
b2sums=('33814828a854838f15e9cb4bc6563daaec940f7eea9e534a4322d64fb4a20ddacff633482c491ceabf951ea5a0fb1214527000345016b8004199524cf0db6b80')

build() {
  cd $_name-$pkgver
  python -m build --wheel --no-isolation
}

# NOTE: all tests are disabled, because they require docker

package() {
  cd $_name-$pkgver
  python -m installer --destdir="$pkgdir" dist/*.whl
  install -vDm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname/"
}
