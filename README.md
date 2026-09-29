# fonts-extended

The full CachyOS desktop font set — Noto CJK + emoji, Cantarell, DejaVu,
Bitstream Vera, Open Sans, Meslo Nerd, and awesome-terminal glyphs — installed
system-wide.

`fonts-extended` installs the CachyOS netinstall "fonts" subgroup on top of the
lean `desktop-fonts` layer. It is deliberately separate from `desktop-fonts` so
the lightweight streaming-desktop images do not pull the heavy CJK set, while a
full KDE workstation wants it. Each family ships as an installed Arch package, so
its presence is verifiable by querying the package database.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `fonts-extended` |
| Requires | `layer-desktop-fonts` (`@github.com/opencharly/layer-desktop-fonts`) |
| Distro | `arch` |
| Packages | `noto-fonts`, `noto-fonts-cjk`, `noto-fonts-emoji`, `cantarell-fonts`, `ttf-bitstream-vera`, `ttf-dejavu`, `ttf-opensans`, `ttf-meslo-nerd`, `awesome-terminal-fonts` |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list:

```yaml
my-kde-workstation:
  candy:
    base: cachyos
    candy:
      - '@github.com/opencharly/layer-fonts-extended:v2026.240.0218'
```

Then, inside the built image:

```bash
pacman -Qi noto-fonts-cjk    # the heavy CJK set this candy is split out for
fc-list | grep -i 'Noto'     # the rendered families
```

## Layout

- `charly.yml` — the `fonts-extended:` candy entity: the `require:` dep, the
  `arch` package arm, and the package `check:` steps.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Base layer: `layer-desktop-fonts`
- Owning skill: `/charly-selkies:fonts-extended` — this layer's full CachyOS
  desktop font set
- Base skill: `/charly-selkies:desktop-fonts` — the lean JetBrains Mono + Nerd
  Fonts base this candy extends
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
