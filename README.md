# ribbit

Speak the X clipboard with Piper, without the one-second model load on
every message. `ribbitd` keeps the voice loaded, listens on a Unix
socket and plays speech itself; `ribbit-speak` sends it text.

## Install (Arch Linux)

`piper-tts` and `piper-voices-en-us` come from the AUR, so `makepkg` can't
install them by itself. Install them first with an AUR helper:

```
yay -S --asdeps piper-tts piper-voices-en-us
```

Then build and install ribbit, which pulls the rest from the official repos:

```
makepkg -si
```

If pacman asks which `onnxruntime` provider to use, pick `onnxruntime-cpu`
unless you want GPU inference.

Playback goes through ALSA's default device. On a PipeWire system that
needs `pipewire-alsa` (on PulseAudio, `pulseaudio-alsa`).

Then start the daemon now and at every login:

```
systemctl --user enable --now ribbitd.service
```

## Use

```
ribbit-speak           # speak the clipboard
ribbit-speak -p        # speak the highlighted text instead
ribbit-speak 0.8       # faster, for this call only (lower is faster)
ribbit-speak --stop    # stop whatever is being spoken
```

Running it again while it's speaking stops it, so one hotkey can start and stop.
New speech interrupts whatever is currently being spoken.

## Protocol

One request per connection to `$XDG_RUNTIME_DIR/ribbit.sock`:

- **Speak:** a line with the length scale (empty for the daemon's
  default), then the text, then close the write side. The daemon closes
  the connection when it finishes speaking. Disconnecting early stops
  the speech.
- **Stop:** the line `stop`.

```
printf '1.0\nHello there.' | nc -NU $XDG_RUNTIME_DIR/ribbit.sock
```

```
printf 'stop\n' | nc -NU $XDG_RUNTIME_DIR/ribbit.sock
```

## Configure

The daemon's options are `--model`, `--socket`, `--sentence-silence`
(default 0.2 s) and `--length-scale`, the default speed (default 1.0,
lower is faster). A speed given to `ribbit-speak` overrides it for that
call. To change them, override the service:

```
systemctl --user edit ribbitd.service
```

```
[Service]
ExecStart=
ExecStart=/usr/bin/ribbitd --length-scale 0.8 --sentence-silence 0.4
```

## Files

| File | Installed to |
|---|---|
| `ribbitd` | `/usr/bin/ribbitd` |
| `ribbit-speak` | `/usr/bin/ribbit-speak` |
| `ribbitd.service` | `/usr/lib/systemd/user/ribbitd.service` |

## Run without installing

```
./ribbitd
```

```
./ribbit-speak
```

## License

MIT. See [LICENSE](LICENSE).
