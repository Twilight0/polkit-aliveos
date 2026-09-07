# Maintainer: Twilight0 <https://github.com/Twilight0>
pkgname=polkit-aliveos
pkgver=1.0.0
pkgrel=1
pkgdesc="Transparent Polkit authentication agent for AliveOS with explicit caller disclosure and Zenity-GTK3 styling"
arch=('any')
url="https://github.com/Twilight0/polkit-aliveos"
license=('GPL-3.0-or-later')
depends=('python' 'python-gobject' 'gtk3' 'polkit' 'libcanberra')
provides=('polkit-authentication-agent')
conflicts=('polkit-gnome')

package() {
  cd "${srcdir}/.."
  
  # Install executables
  install -Dm755 polkit-aliveos "${pkgdir}/usr/lib/polkit-aliveos/polkit-aliveos"
  install -Dm755 polkit-aliveos-config "${pkgdir}/usr/bin/polkit-aliveos-config"

  # Symlink agent binary
  install -d "${pkgdir}/usr/bin"
  ln -sf /usr/lib/polkit-aliveos/polkit-aliveos "${pkgdir}/usr/bin/polkit-aliveos"

  # Install documentation
  install -Dm644 README.md "${pkgdir}/usr/share/doc/${pkgname}/README.md"
}
