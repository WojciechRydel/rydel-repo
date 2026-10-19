# Maintainer: Wojciech Rydel <wojciech@rydel.xyz>
pkgname=rydel-tools
pkgver=1.0.0
pkgrel=1
pkgdesc="Personal Wayland typing helpers: type-text, pass-type, and KeePassXC pickers"
arch=('any')
url="https://github.com/WojciechRydel/rydel-repo"
license=('MIT')
depends=(
  'bash'
  'bemenu'
  'fzf'
  'keepassxc'
  'libnotify'
  'pass'
  'sudo'
  'wl-clipboard'
  'wtype'
  'ydotool'
)
options=('!strip' '!debug')

package() {
  cd "$startdir"

  install -Dm755 type-text "$pkgdir/usr/bin/type-text"
  install -Dm755 pass-type "$pkgdir/usr/bin/pass-type"
  install -Dm755 kp-type   "$pkgdir/usr/bin/kp-type"
  install -Dm755 kp-fzf    "$pkgdir/usr/bin/kp-fzf"
  install -Dm644 kp-lib    "$pkgdir/usr/bin/kp-lib"

  install -Dm644 ydotool.service.d/type-text.conf \
    "$pkgdir/usr/lib/systemd/user/ydotool.service.d/type-text.conf"
}
