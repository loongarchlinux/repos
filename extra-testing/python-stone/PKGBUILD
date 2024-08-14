# Maintainer:

pkgname=python-stone
_name=${pkgname#python-}
pkgver=3.3.8
pkgrel=1
pkgdesc='The Official API Spec Language for Dropbox API V2'
arch=(any)
url='https://github.com/dropbox/stone'
license=(MIT)
depends=(
  python
  python-packaging
  python-ply
  python-six
)
makedepends=(
  git
  python-build
  python-installer
  python-setuptools
  python-wheel
)
checkdepends=(python-pytest)
source=("git+$url#tag=v$pkgver")
sha256sums=('2a8c1d53f9bc1feaeafc5aa3e2992d6f8062b4f49773aedb795cb46bfd3fb427')

# Remove pytest-runner from setup_requires
prepare() {
  sed -e '/pytest-runner/d' -i "$_name"/setup.py
}

build() {
  cd "$_name"
  python -m build --wheel --no-isolation
}

check() {
  cd "$_name"
  pytest -vv
}

package() {
  cd "$_name"
  python -m installer --destdir="$pkgdir" dist/*.whl

  # Symlink license file
  local site_packages=$(python -c "import site; print(site.getsitepackages()[0])")
  install -d "$pkgdir"/usr/share/licenses/$pkgname
  ln -s "$site_packages"/"$_name"-$pkgver.dist-info/LICENSE \
    "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
