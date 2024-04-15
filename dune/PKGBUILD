pkgname=dune
pkgver=3.15.0
pkgrel=1
pkgdesc="A composable build system for OCaml (formerly jbuilder)"
arch=('x86_64')
url="https://github.com/ocaml/dune"
license=('Apache')
depends=('glibc')
makedepends=('ocaml')
optdepends=('ocaml: Dune standard library')
source=("${url}/archive/${pkgver}/${pkgname}-${pkgver}.tar.gz")
b2sums=('SKIP')

_dune_release_pkgs=('dune' 'dune-action-plugin' 'dune-build-info' 'dune-configurator' 'dune-glob' 'dune-private-libs'
                    'dune-site' 'dune-rpc' 'dyn' 'stdune' 'ordering' 'xdg' 'chrome-trace' 'ocamlc-loc')

build() {
    cd "${srcdir}/${pkgname}-${pkgver}/"

    ./configure --libdir="/usr/lib/ocaml/"

    make "_boot/dune.exe"

    local dune_release_pkgs='dummy'
    for _pkg in "${_dune_release_pkgs[@]}"; do
      dune_release_pkgs+=",${_pkg}"
    done
    dune_release_pkgs="${dune_release_pkgs#dummy,}"
    echo "Building packages: ${dune_release_pkgs}"

    ./dune.exe build -p "${dune_release_pkgs}" --profile="dune-bootstrap"
}

package() {
    cd "${srcdir}/${pkgname}-${pkgver}/"

	for _pkg in "${_dune_release_pkgs[@]}"; do
      ./dune.exe install "${_pkg}" --destdir="${pkgdir}/" --prefix="/usr/" --libdir="/usr/lib/dune/"
    done

    install -d "${pkgdir}/usr/share/"
    mv "${pkgdir}"/usr/{doc/,share/}
    mv "${pkgdir}"/usr/{man/,share/}
    install -dm755 "${pkgdir}/usr/share/licenses/${pkgname}/"
    ln -s "/usr/share/doc/pp/LICENSE.md" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
