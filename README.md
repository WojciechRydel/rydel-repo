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

## Configuration

The scripts carry no machine-specific values. KeePassXC paths are read from
the environment or `~/.config/rydel-tools/config`; a template is provided in
[`config.example`](config.example):

```sh
mkdir -p ~/.config/rydel-tools
cp config.example ~/.config/rydel-tools/config
$EDITOR ~/.config/rydel-tools/config
```

`pass-type` honors the standard `PASSWORD_STORE_DIR` (default
`~/.password-store`).

## Building

```sh
makepkg -f
```

Packages are built and published to the `gh-pages` branch by
`.github/workflows/publish.yml` on every push to `main`.

## License

MIT
