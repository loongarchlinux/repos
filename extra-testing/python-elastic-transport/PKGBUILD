# Maintainer: Carl Smedstad <carsme@archlinux.org>

pkgname=python-elastic-transport
_pkgname=elastic-transport-python
pkgver=8.15.0
pkgrel=1
pkgdesc="Transport classes and utilities shared among Python Elastic client libraries"
arch=(any)
url="https://github.com/elastic/elastic-transport-python"
license=(Apache-2.0)
depends=(
  python
  python-aiohttp
  python-certifi
  python-httpx
  python-orjson
  python-requests
  python-typing_extensions
  python-urllib3
)
makedepends=(
  python-build
  python-installer
  python-setuptools
  python-wheel
)
checkdepends=(
  python-pytest
  python-pytest-asyncio
  python-pytest-httpserver
  python-respx
  python-trustme
)
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('a9d8b250bf646252de7ada32c96e289ed8853fb72a28f9bec64ba78220d11539')

build() {
  cd $_pkgname-$pkgver
  python -m build --wheel --no-isolation
}

check() {
  cd $_pkgname-$pkgver
  # OpenTelemetry not in Arch repos (yet)
  pytest --override-ini="addopts=" --ignore tests/test_otel.py
}

package() {
  cd $_pkgname-$pkgver
  python -m installer --destdir="$pkgdir" dist/*.whl
}
