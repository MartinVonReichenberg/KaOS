pkgname=bitwarden-cli
_pkgname=bw
pkgver=2024.3.1
pkgrel=1
pkgdesc='Open source password management solution for individuals, teams, and business organizations - The CLI only variant'
arch=('x86_64')
url='https://github.com/bitwarden/cli'
license=('GPL3')
depends=('gcc-libs')
makedepends=('unzip')
options=('!strip')
source=("${pkgname}-${pkgver}.zip::https://github.com/bitwarden/clients/releases/download/cli-v${pkgver}/${_pkgname}-linux-${pkgver}.zip")
sha512sums=('SKIP')

package() {
    mkdir -p "${pkgdir}/usr/bin/"
    bsdtar -xf "${srcdir}/${pkgname}-${pkgver}.zip" -C "${pkgdir}/usr/bin/"

    msg2 "Make sure the binary is executable within system"
    chmod 0755 "${pkgdir}/usr/bin/${_pkgname}"

    msg2 "Linking binary from SOURCE to another name - bitwarden-cli"
    ln -v -f -s "/usr/bin/${_pkgname}" "${pkgdir}/usr/bin/${pkgname}"

    msg2 "Adding support for ZSH SHELL Completions"
    ${srcdir}/${_pkgname} completion --shell zsh > "${srcdir}/zsh-completion" 2> "/dev/null"
    install -Dm644 "${srcdir}/zsh-completion" "${pkgdir}/usr/share/zsh/vendor-completions/_${pkgname}"
}
