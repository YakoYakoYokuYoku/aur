# Maintainer: Luis Martinez <luis dot martinez at disroot dot org>

pkgname=python-deepl
pkgver=1.5.0
pkgrel=1
pkgdesc="DeepL language translation API"
arch=('any')
url="https://github.com/deeplcom/deepl-python"
license=('MIT')
depends=('python-requests')
makedepends=('git' 'python-poetry-core' 'python-build' 'python-installer')
install=deepl.install
changelog=CHANGELOG.md
source=("$pkgname::git+$url#tag=v$pkgver?signed")
sha256sums=('SKIP')
validpgpkeys=('DBDC63E97C526204335805941FA7A782EC90634E') ## Daniel Jones

build() {
	cd "$pkgname"
	python -m build --wheel --no-isolation
}

## tests require a DeepL API key (paid account)

package() {
	export PYTHONHASHSEED=0
	cd "$pkgname"
	python -m installer --destdir="$pkgdir/" dist/*.whl
	install -Dm644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname/"
}
