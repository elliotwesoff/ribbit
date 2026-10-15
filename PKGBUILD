# Maintainer: Elliot <ewesoff@gmail.com>
pkgname=ribbit
pkgver=0.2.0
pkgrel=1
pkgdesc="Speak the X clipboard with a Piper voice kept loaded in a local daemon"
arch=('any')
license=('unknown')
depends=(
  'alsa-utils'          # aplay
  'bash'
  'openbsd-netcat'      # nc -N -U
  'piper-tts'           # AUR
  'piper-voices-en-us'  # AUR
  'python'
  'xclip'
)
optdepends=(
  'pipewire-alsa: play through PipeWire'
  'pulseaudio-alsa: play through PulseAudio'
)
source=(
  'ribbitd'
  'ribbitd.service'
  'ribbit-speak'
)
# Local files that change during development, so they aren't pinned.
sha256sums=('SKIP' 'SKIP' 'SKIP')

package() {
  install -Dm755 ribbitd "$pkgdir/usr/bin/ribbitd"
  install -Dm755 ribbit-speak "$pkgdir/usr/bin/ribbit-speak"
  install -Dm644 ribbitd.service "$pkgdir/usr/lib/systemd/user/ribbitd.service"
}
