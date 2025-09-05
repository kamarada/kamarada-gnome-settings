# Maintainer: Antonio Medeiros <linuxkamarada@gmail.com>
# Contributor: Mark Wagie <mark at manjaro dot org>
# Contributor: Stefano Capitani  <stefanoatmanjarodotorg>
# Contributor: Ramon Buldó

pkgname=(
  'kamarada-gnome-settings'
  'kamarada-gnome-extension-settings'
)
pkgbase=kamarada-gnome-settings-src
pkgver=20250504
pkgrel=1
arch=('any')
url="https://github.com/kamarada/kamarada-gnome-settings"
license=('GPL-3.0-or-later')
makedepends=('git')
_commit=1fabeca59a200f1b801a2fff1ded2d791231d004
source=("git+https://github.com/kamarada/kamarada-gnome-settings-src.git#commit=${_commit}")
sha256sums=('SKIP')
#validpgpkeys=('688E8F82879D0E25CE541426150C200743ED46D8') # Mark Wagie <mark@manjaro.org>

pkgver() {
  cd "${pkgbase}"
  git show -s --format=%cd --date=format:%Y%m%d HEAD
}

package_kamarada-gnome-settings() {
  pkgdesc="Linux Kamarada GNOME settings"
  depends=(
    'accent-color-change'
    'adw-gtk-theme'
    'bibata-cursor-theme'
    'kamarada-gnome-backgrounds'
    'manjaro-base-skel'
    'papirus-maia-icon-theme'
    'ttf-hack-nerd'
    'ttf-meslo-nerd-font-powerlevel10k'
  )
  optdepends=(
    'kvantum-manjaro: for KvLibadwaitaMaia theme'
    'qt5ct: Qt 5 theming'
    'qt6ct: Qt 6 theming'
  )
  provides=(
    'manjaro-desktop-settings'
    'manjaro-gnome-settings'
  )
  conflicts=(
    'manjaro-gnome-settings-gnome-next'
    'manjaro-gnome-settings-19.0'
    'manjaro-gnome-assets'
    'manjaro-gdm-theme'
    'firefox-gnome-theme-maia'
    'adwaita-maia'
    'manjaro-gdm-branding'
    'manjaro-gnome-settings'
  )
  replaces=(
    'manjaro-gnome-settings-gnome-next'
    'manjaro-gnome-assets'
    'manjaro-gdm-branding'
    'manjaro-gnome-settings'
  )
  install='settings.install'

  cd "${pkgbase}"
  install -Dm644 schemas/99_manjaro-settings.gschema.override -t \
    "${pkgdir}"/usr/share/glib-2.0/schemas/

  install -Dm644 dconf/user -t "${pkgdir}"/etc/dconf/profile/
  install -Dm644 dconf/gdm -t "${pkgdir}"/etc/dconf/profile/
  install -Dm644 dconf/00_app_folder_defaults -t "${pkgdir}"/etc/dconf/db/local.d/

  # Kvantum
  install -Dm644 xdg/Kvantum/kvantum.kvconfig -t "${pkgdir}/etc/xdg/Kvantum/"

  # Logind
  install -Dm644 systemd/logind.conf.d/21-kill-user-processes.conf -t \
    "${pkgdir}/etc/systemd/logind.conf.d/"

  # Misc defaults
  cp -r profile.d skel "${pkgdir}"/etc/

  # Qt5Ct (not currently used)
#  install -Dm644 colors/Adwaita{-maia.conf,-maia-dark.conf} -t \
#    "${pkgdir}"/usr/share/qt5ct/colors/
#  install -Dm644 colors/Adwaita{-maia.conf,-maia-dark.conf} -t \
#    "${pkgdir}"/usr/share/qt6ct/colors/
}

package_kamarada-gnome-extension-settings() {
  pkgdesc="Linux Kamarada GNOME extensions settings"
  depends=(
    'gnome-shell-extensions'
    'kamarada-gnome-settings'
  )
  optdepends=(
    'gnome-browser-connector: browser connecter for extensions website'
  )
  provides=(
    'manjaro-gnome-extension-settings'
  )
  conflicts=(
    'gnome-shell-extension-custom-accent-colors'
    'manjaro-gnome-extension-settings-gnome-next'
    'manjaro-gnome-extension-settings'
  )
  replaces=(
    'manjaro-gnome-extension-settings-gnome-next'
    'manjaro-gnome-extension-settings'
  )
  install=schemas.install

  cd "${pkgbase}"

  # Extension overrides

  schemas=(
    org.gnome.shell.extensions.arcmenu  # ArcMenu
    org.gnome.shell.extensions.dash-to-dock  # Dash to Dock
    org.gnome.shell.extensions.dash-to-panel  # Dash to Panel
    org.gnome.shell.extensions.gnome-ui-tune  # GNOME 4x UI Improvements
    org.gnome.shell.extensions.user-theme  # User Themes
  )

  for schema in ${schemas[*]}; do
    install -Dm644 schemas/${schema}.gschema.override -t \
      "${pkgdir}"/usr/share/glib-2.0/schemas/
  done
}

#package_manjaro-gnome-minimal-settings() {
#  pkgdesc='Manjaro Linux gnome-minimal settings'
#  depends=()
#  provides=('manjaro-desktop-settings')

#  cd "${pkgbase}"
#  ?
#}
