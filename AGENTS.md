# AGENTS.md — layer-fonts-extended

Standalone candy repo for the `fonts-extended` layer — the full CachyOS desktop
font set (Noto CJK + emoji, Cantarell, DejaVu, Bitstream Vera, Open Sans, Meslo
Nerd, awesome-terminal glyphs) on top of the lean `desktop-fonts` layer. The
candy lives in `charly.yml` at the repo root: the `require:` dep on
`layer-desktop-fonts`, the `arch` package arm, and the package `check:` steps. It
carries **no `skill:` entity**, so no owning `/charly-<family>:<name>` skill is
projected into the marketplace corpus.

Canonical files:

- `charly.yml` — the `fonts-extended:` candy entity (no `skill:` entity present).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-selkies:desktop-fonts` — the closest owning skill: the lean JetBrains
  Mono + Nerd Fonts base this candy extends, and the font-family reference. Load
  before editing or troubleshooting the layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, package
  sections). Load before editing any entity field or plan step.

There is no dedicated `/charly-*:fonts-extended` owning skill — this repo's candy
carries no `skill:` entity. The gap is recorded against
`opencharly/opencharly#291`; when one is authored, add it here.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence: each font
  family asserted as an installed `arch` package (`noto-fonts-cjk` is the one the
  candy is split out for). They must stay valid on the `arch` arm they run on.
- The split from `desktop-fonts` is deliberate — the heavy CJK set must not leak
  into the lightweight streaming-desktop images.

## Modify this repo

- Edit the `fonts-extended:` candy entity in `charly.yml`. The `require:` dep pins
  the lean font base; a font-family change belongs in the `plan:` as an
  observable package `check:` step.
- Keep the candy Arch-only unless the package set is confirmed available on
  another distro.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
