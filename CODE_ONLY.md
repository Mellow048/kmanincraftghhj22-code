# Code-only snapshot

This repository is a **code-only mirror** of
[`Mellow048/kmanincraftghhj22`](https://github.com/Mellow048/kmanincraftghhj22),
taken from `main` at commit `7a8aa4b` ("Remove stale DEEPSEEK-MASTERPROMPT.md token bloat"),
after the **Remaster v3/v3.5** upgrade in `9f0dd5b`.

It exists so the full source can be read, edited, and remastered without moving the
4.1 GB of tracked media in the original repository.

## Scope

The three remaster targets are included in full:

| Topic | Path | What is here |
| --- | --- | --- |
| In This Town | `Topics/InThisTown/` | Pack source, staging, characters, places, shots, sound notes, template |
| Server Lore | `Topics/ServerLore/` | Pack source, cast, props, places, script, shots, sound notes, template |
| Explainer | `Topics/Explainer/` | Pack source, cast, props, charts, money, stage, script, shots, sound notes, template |

Every film under `src/videos/` that uses those packs is included too, along with the
shared engine (`src/engine/`), scripts, tests, docs, and GitHub Actions workflows.

This snapshot includes the Remaster v3/v3.5 changes: grounded lie/sleep poses,
`cam.front` / `cam.twoShot` / `cam.fitWidth`, the new back-of-character, blocking,
9:16 over-zoom and phasing direction gates, the rebuilt ServerLore and Explainer
templates, and Explainer's six physical metaphor props. See
`docs/REMASTER-V3-CHANGELOG.md`.

## What was left out

All binary media and generated output, about **4.1 GB / 876 files**:

- `*.mp4`, `*.mov`, `*.webm` — finished renders, reference films, review clips
- `*.mp3`, `*.wav`, `*.m4a`, `*.aac` — narration, mixes, sound effects
- `*.png`, `*.jpg`, `*.jpeg`, `*.gif`, `*.webp` — contact sheets, stills, reference images
- `*.zip` and other archives
- `renders/`, `review/`, `.cache-sheets/`, `out/`, `node_modules/`

Text artifacts are kept, including `public/audio/**/*.words.json` alignment data and
all `.md`, `.json`, `.ts`, `.tsx`, `.py`, `.mjs`, and `.yml` files.

The original repository is unchanged and remains the source of truth for every asset.

## Restoring media for a render

Media is **not** committed here. Pull it from the original repository on demand:

```bash
bash scripts/restore-assets.sh
```

That script does a shallow, blob-filtered sparse checkout of
`Mellow048/kmanincraftghhj22`, copies `public/audio/` into this working tree, and
fetches the four topic-level music files (`InThisTownMusic.aac`, `up_happy.m4a`,
`up_sad.m4a`, `explainer_bgm_loop.wav`). Use `--with-references` to also copy the
three topics' reference films, or `--force` to refresh audio that is already present.

Generated audio from `.github/workflows/tts.yml` can also be dropped into
`public/audio/<composition>/` without restoring the old mix.

## Rendering

Rendering must run in GitHub Actions, not on a local machine.

Use **Actions → Render code-only film** (`.github/workflows/render-code.yml`):

1. Enter the Remotion composition id (for example `in-this-town-we-live-at-the-bottom`).
2. Optionally enter a frame range for a short review clip.
3. Run the workflow.

The workflow installs dependencies, restores the audio assets, runs typecheck/check/rehearse,
renders with software GL, and uploads the MP4 as a build artifact. Nothing is committed
back, so this repository stays code-only.

The inherited workflows (`render-one.yml`, `render-preview.yml`, `render.yml`, `stills.yml`)
also work, but they expect `public/audio/` to exist. Run `scripts/restore-assets.sh`
in the job first if you use them.

## Editing notes

- Do not commit MP4s, audio, images, or `out/` to this repository.
- `AGENTS.md` and `CLAUDE.md` contain the house rules for the engine and film structure.
- `Topics/InThisTown/PACK.md`, `Topics/ServerLore/PACK.md`, and
  `Topics/Explainer/PACK.md` catalogue the available parts.
- Each film has `SCRIPT.md`, `SHOTS.md`, and `SOUND.md` next to its source; start there.
- `npm run typecheck`, `npm run check`, and `npm run test:direction` are the fast guards.
- With no audio restored, `npm run check` reports missing mixes as notes instead of
  failures. After `scripts/restore-assets.sh`, a missing or stale mix fails again.
