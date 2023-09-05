# Maintainer: Daniel M. Capella <polyzen@archlinux.org>

pkgname=jedi-language-server
pkgver=0.41.0
pkgrel=1
pkgdesc='Language server for Jedi'
arch=('any')
url=https://github.com/pappasam/jedi-language-server
license=('MIT')
depends=(
  'python-docstring-to-markdown'
  'python-jedi'
  'python-pydantic'
  'python-pygls'
)
makedepends=('python-build' 'python-installer' 'python-poetry-core')
checkdepends=('python-lsp-jsonrpc' 'python-pyhamcrest' 'python-pytest')
source=("$url/archive/v$pkgver/$pkgname-$pkgver.tar.gz")
b2sums=('3bd112f17665e5d2273c3c880697c5f4aa7335b8f29b770e00a61a3204a619cd51d14bdf6ae6b3fce1193b816c3177670088447ba4bb1b783027072f419a1a9d')

prepare() {
  cd $pkgname-$pkgver
  # Remove include list https://github.com/pypa/wheel/issues/92
  sed -i '/include = \["README.md"\]/d' pyproject.toml
}

build() {
  cd $pkgname-$pkgver
  python -m build --wheel --skip-dependency-check --no-isolation
}

check() {
  cd $pkgname-$pkgver
  mkdir -p temp
  local site_packages=$(python -c "import site; print(site.getsitepackages()[0])")
  python -m installer --destdir=temp dist/*.whl
  PATH="$PWD/temp/usr/bin:$PATH" PYTHONPATH="$PWD/temp/$site_packages" pytest tests
}

package() {
  cd $pkgname-$pkgver
  python -m installer --destdir="$pkgdir" dist/*.whl

  # Symlink license file
  local site_packages=$(python -c "import site; print(site.getsitepackages()[0])")
  install -d "$pkgdir"/usr/share/licenses/$pkgname
  ln -s "$site_packages"/${pkgname//-/_}-$pkgver.dist-info/LICENSE \
    "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
