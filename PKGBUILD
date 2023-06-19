# Maintainer: Bennett Petzold <dansecob.aur gmail com>

pkgname='qsv'
pkgver='0.107.0'
pkgrel='1'
pkgdesc='A command line program for CSV files. Fork of xsv.'
arch=('any')
url='https://github.com/jqnatividad/qsv'
license=('MIT' 'Unlicense')
depends=('python>=3.8'
         'docopt-wordlist')
makedepends=('cargo')
optdepends=('bash-completion: tab completion for bash')
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/$pkgver.tar.gz"
        'completion.patch')

md5sums=('c0de494ec2a91fed3641a8d79443c9fb'
         'b6ac3fc857e4d2657be8c4e81c86a56c')
sha512sums=('dbee37b005253a2201e9efdbd9aabe742a16a98b18406a40c1775354ea9c4c222a4d670c479fda1b4a38e15b14dae5289a72c2394a682432bb617be143f6ab41'
            '809cd1ad542319a8f98c061b222e386afe90668acdc3b4f9183aa5cb3d3e70548fd72d2a160841072fc6ab29d6cd6d1f6c0596f19451dc21ff63449d00b7d2db')

prepare() {
    cd $pkgname-$pkgver
    patch --forward --strip=1 --input="${srcdir}/completion.patch"
    cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
    cd $pkgname-$pkgver
    export RUSTUP_TOOLCHAIN=stable
    export CARGO_TARGET_DIR=target
    cargo build --frozen --release --features feature_capable,apply,fetch,foreach,generate,luau,polars,python,to
}

check() {
    cd $pkgname-$pkgver
    export RUSTUP_TOOLCHAIN=stable
    cargo test --frozen --features feature_capable,apply,fetch,foreach,generate,luau,polars,python,to
}

package() {
    cd $pkgname-$pkgver
    install -Dm0755 -t "$pkgdir/usr/bin/" "target/release/$pkgname"
    install -Dm0644 -T "scripts/docopt-wordlist.bash" "$pkgdir/usr/share/bash-completion/completions/qsv"
}
