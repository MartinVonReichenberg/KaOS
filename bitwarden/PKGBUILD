pkgname=bitwarden
_pkgname=Bitwarden
pkgver=2024.4.1
pkgrel=1
pkgdesc='Open source password management solutions for individuals, teams, and business organizations.'
arch=('x86_64')
url="https://bitwarden.com/"
depends=('libnotify' 'libsecret' 'libxtst' 'libxss' 'nss')
license=('custom' 'GPL-3')
source=("${pkgname}-${pkgver}.rpm::https://github.com/bitwarden/clients/releases/download/desktop-v${pkgver}/Bitwarden-${pkgver}-x86_64.rpm"
		"https://github.com/bitwarden/clients/releases/download/desktop-v${pkgver}/latest-linux.yml")
sha512sums=('SKIP' 'SKIP')
options=('!strip' '!emptydirs')

package() {
	mkdir -p "${pkgdir}/"
	bsdtar -xf "${srcdir}/${pkgname}-${pkgver}.rpm" -C "${pkgdir}/"

	msg2 "Removing unnecessary file properties from the RPM binary package"
	rm -drf "${pkgdir}/usr/lib/"

	msg2 "Linking binaries from SOURCE to the system"
	install -d "${pkgdir}/usr/bin/"
	ln -v -s -f "/opt/${_pkgname}/${pkgname}" --target-directory="${pkgdir}/usr/bin/"

	sed -i \
	-e "/Exec=/i\Path=/opt/Bitwarden/\nTryExec=bitwarden" \
	-e "s|Exec=/opt/Bitwarden/bitwarden %U|Exec=/usr/bin/bitwarden %U|g" "${pkgdir}/usr/share/applications/${pkgname}.desktop"

	msg2 "Installing Electron & Chromium LICENSEs into the system"
	install -Dm644 ${pkgdir}/opt/${_pkgname}/{LICENSE.electron.txt,LICENSES.chromium.html} -t "${pkgdir}/usr/share/licenses/${pkgname}/"

	msg2 "Imposing sandboxing by modifying SUID properties"
	chmod -v 4755 ${pkgdir}/opt/${_pkgname}/{chrome-sandbox,chrome_crashpad_handler}

	msg2 "ALL DONE"
}
