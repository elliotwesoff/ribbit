# Maintainer: Elliot <ewesoff@gmail.com>
pkgname=ribbit
pkgver=0.2.1
pkgrel=1
pkgdesc="Speak the X clipboard with a Piper voice kept loaded in a local daemon"
arch=('any')
license=('MIT')
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
  'LICENSE'
  'ribbitd'
  'ribbitd.service'
  'ribbit-speak'
)
# Regenerate after editing any source file: makepkg -g
sha256sums=('4e54283892708a34e8c78bb65403e992ff2c9d6f37f143356cc88fa35d98f160'
            '9d416e547dcd96176242622295c8c5d693976c38bffc433e94083d5c4b73081b'
            '96fb01da84e84672126c692632bff862ca6ef725000b50639fa9208be885a33b'
            'f46fd02e51758493b14b4a04aafc5bf54b30671c3306eca785dd72aeff98d1c5')

package() {
  install -Dm755 ribbitd "$pkgdir/usr/bin/ribbitd"
  install -Dm755 ribbit-speak "$pkgdir/usr/bin/ribbit-speak"
  install -Dm644 ribbitd.service "$pkgdir/usr/lib/systemd/user/ribbitd.service"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
