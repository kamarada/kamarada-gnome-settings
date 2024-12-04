# Maintainer: Mark Wagie <mark at manjaro dot org>
# Contributor: Stefano Capitani  <stefanoatmanjarodotorg>
# Contributor: Ramon Buldó

pkgname=(
  'manjaro-gnome-settings'
  'manjaro-gnome-extension-settings'
)
pkgbase=manjaro-gnome-settings
pkgver=20241204
pkgrel=2
arch=('any')
url="https://gitlab.manjaro.org/profiles-and-settings/manjaro-gnome-settings"
license=('GPL-3.0-or-later')
makedepends=('git')
_commit=8c48ff5962b6b3a0920443dc43201f7a016292e5  # branch/master
source=("git+https://gitlab.manjaro.org/profiles-and-settings/manjaro-gnome-settings.git#commit=${_commit}?signed")
sha256sums=('1292193229ae835dacfb202ac18bfde5792ca7751969b33b8bd3891848d7ba25')
validpgpkeys=('688E8F82879D0E25CE541426150C200743ED46D8') # Mark Wagie <mark@manjaro.org>

pkgver() {
  cd "${pkgbase}"
  git show -s --format=%cd --date=format:%Y%m%d HEAD
}

package_manjaro-gnome-settings() {
  pkgdesc="Manjaro Linux GNOME settings"
  depends=(
    'accent-color-change'
    'adw-gtk-theme'
    'bibata-cursor-theme'
    'manjaro-gnome-backgrounds'
    'manjaro-base-skel'
    'papirus-icon-theme'
    'ttf-hack'
  )
  optdepends=(
    'kvantum-manjaro: for KvLibadwaitaMaia theme'
    'lighter-gnome: disable some gnome-settings-daemon components'
    'papirus-maia-icon-theme: for Maia folder color'
    'qt5ct: Qt 5 theming'
    'qt6ct: Qt 6 theming'
  )
  provides=('manjaro-desktop-settings')
  conflicts=(
    'manjaro-gnome-settings-gnome-next'
    'manjaro-gnome-settings-19.0'
    'manjaro-gnome-assets'
    'manjaro-gdm-theme'
    'firefox-gnome-theme-maia'
    'adwaita-maia'
    'manjaro-gdm-branding'
  )
  replaces=(
    'manjaro-gnome-settings-gnome-next'
    'manjaro-gnome-assets'
    'manjaro-gdm-branding'
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

package_manjaro-gnome-extension-settings() {
  pkgdesc="Manjaro Linux GNOME extensions settings"
  depends=(
    'gnome-shell-extensions'
    'manjaro-gnome-settings'
  )
  optdepends=(
    'gnome-browser-connector: browser connecter for extensions website'
  )
  conflicts=(
    'gnome-shell-extension-custom-accent-colors'
    'manjaro-gnome-extension-settings-gnome-next'
  )
  replaces=(
    'manjaro-gnome-extension-settings-gnome-next'
  )
  install=schemas.install

  cd "${pkgbase}"

  # Extension overrides

  schemas=(
    org.gnome.shell.extensions.arcmenu  # ArcMenu
    org.gnome.shell.extensions.dash-to-dock  # Dash to Dock
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
