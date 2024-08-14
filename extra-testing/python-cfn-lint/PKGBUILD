# Maintainer: Chih-Hsuan Yen <yan12125@archlinux.org>

pkgname=python-cfn-lint
# https://github.com/aws-cloudformation/cfn-lint/blob/main/CHANGELOG.md
pkgver=1.9.6
pkgrel=1
pkgdesc='CloudFormation Linter'
arch=(any)
url='https://github.com/aws-cloudformation/cfn-lint'
# https://github.com/aws-cloudformation/cfn-lint/blob/v0.84.0/setup.py#L63 uses "MIT no attribution",
# which corresponds to https://spdx.org/licenses/MIT-0.html
license=('MIT-0')
depends=(python python-yaml python-aws-sam-translator
         python-jsonpatch python-networkx
         python-sympy python-regex
         python-typing_extensions)
makedepends=(git python-build python-installer python-setuptools python-wheel)
checkdepends=(python-pytest python-defusedxml
              python-pydot python-junit-xml python-jschema-to-python python-sarif-om)
optdepends=(
  'python-pydot: for building graphs from templates'
  'python-junit-xml: for junit formatter'
  'python-jschema-to-python: for sarif formatter'
  'python-sarif-om: for sarif formatter'
)
source=("git+https://github.com/aws-cloudformation/cfn-lint.git#tag=v$pkgver")
sha256sums=('7e3e1e67c7bf025416c1e265afeeae38b25aa2ba5da84c63d505ee4127293fc1')

build() {
  cd cfn-lint
  python -m build --wheel --no-isolation
}

check() {
  cd cfn-lint

  # Tests in test/integration need the cfn-lint binary
  python -m installer --destdir="$PWD/tmp_install" dist/*.whl

  export PYTHONPATH="$PWD/src"
  export PATH="$PATH:$PWD/tmp_install/usr/bin"
  pytest
}

package() {
  cd cfn-lint
  python -m installer --destdir="$pkgdir" dist/*.whl

  install -Dm644 LICENSE -t "$pkgdir"/usr/share/licenses/$pkgname
}
