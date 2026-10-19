# rydel-repo

Personal Arch package repository, served from GitHub Pages.

## Package: `rydel-tools`

Installs the personal typing helpers:

| File | Purpose |
|------|---------|
| `type-text` | Type stdin as keystrokes (ydotool first, wtype fallback, clipboard last). |
| `pass-type` | Pick a `pass` entry with bemenu and type it. Binding: `$mod+Ctrl+s`. |
| `kp-type` | Pick a KeePassXC entry with bemenu and type it. Binding: `$mod+Ctrl+k`. |
| `kp-fzf` | Pick a KeePassXC entry with fzf and copy it (TTY use). |
| `kp-lib` | Shared helpers sourced by `kp-type` / `kp-fzf`. |
| `ydotool.service.d/type-text.conf` | Drop-in so `ydotool.service` retries until the `/dev/uinput` ACL is ready. |

Scripts are installed to `/usr/bin`; the drop-in to
`/usr/lib/systemd/user/ydotool.service.d/type-text.conf`.

## Add the repository

Add to `/etc/pacman.conf`:

```ini
[rydel]
SigLevel = Optional TrustAll
Server = https://wojciechrydel.github.io/rydel-repo
```

Then:

```sh
sudo pacman -Sy
sudo pacman -S rydel-tools
systemctl --user enable --now ydotool.service
```

The `ydotool.service` user unit ships with the `ydotool` package; this package
only provides the retry drop-in, so enable the unit yourself once per user.

## Building

```sh
makepkg -f
```

Packages are built and published to the `gh-pages` branch by
`.github/workflows/publish.yml` on every push to `main`.

## License

MIT
