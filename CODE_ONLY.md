# Code-only snapshot

This repository is a **code-only mirror** of
[`Mellow048/kmanincraftghhj22`](https://github.com/Mellow048/kmanincraftghhj22),
taken from `main` at commit `4b44809` ("Apply Remaster v7 final framework"),
after the Remaster v5 pass in `5e299ad`, Remaster v4 in `ba67946`, Batch 2 films
in `ea23489`, Remaster v3/v3.5 in `9f0dd5b`, and the v3.6 reference-study pass
in `1aceeba`.

It exists so the full source can be read, edited, and remastered without moving the
4.1 GB of tracked media in the original repository.

## Scope

The three remaster targets are included in full:

| Topic | Path | What is here |
| --- | --- | --- |
| In This Town | `Topics/InThisTown/` | Pack source, staging, characters, places, shots, sound notes, template |
| Server Lore | `Topics/ServerLore/` | Pack source, cast, props, places, script, reference scripts, shots, sound notes, template |
| Explainer | `Topics/Explainer/` | Pack source, cast, props, charts, money, stage, script, reference study, shots, sound notes, template |

Every film under `src/videos/` that uses those packs is included too, along with the
shared engine (`src/engine/`), scripts, tests, docs, and GitHub Actions workflows.

This snapshot includes the Remaster v3/v3.5 changes: grounded lie/sleep poses,
`cam.front` / `cam.twoShot` / `cam.fitWidth`, the new back-of-character, blocking,
9:16 over-zoom and phasing direction gates, the rebuilt ServerLore and Explainer
templates, and Explainer's six physical metaphor props. See
`docs/REMASTER-V3-CHANGELOG.md`.

The v3.6 pass adds:

- `Topics/ServerLore/REFERENCE-SCRIPTS.md` — both 50k+ reference transcripts, the
  plain-English formula, banned AI-slop rewrites, and the 9-beat hook-to-CTA skeleton
- `Topics/Explainer/REFERENCE-STUDY.md` — the Inflation reference's 8-step flow,
  character motion, camera grammar, and seamless loop
- `docs/COMPETITOR-STUDY-NEVER-WALK-ALONE.md` — full transcript, concrete-number
  cadence study, and 4-layer payoff anatomy
- Free `edge-tts` lock (never ElevenLabs), caption `y: 0.72` alignment, and two
  direction-test camera fixes

## Remaster v4

The v4 framework pass adds:

- Edge-TTS default `+0%` and `0.42s` breath gaps between narration clips
- Louder background music: InThisTown/Explainer `-13`, ServerLore `-12`
- `cam.front` default `dist: 6.2` / `to: 4.4` for unclipped 9:16 framing
- 3D text width clamping and extra pixel-font glyphs (`=`, `/`, `$`, `()`, `#`, `&`, `—`)
- `docs/CRITIQUE-V4-QUALITY-GATES.md` and `SMALL-MODEL-RENDER-GUIDE.md`
- Three Batch 2 film scaffolds: `taxes-explained-using-minecraft`,
  `the-player-who-never-left-the-spawn-bench`, and `in-this-town-you-cant-drop-your-torch`

## Remaster v5

- New camera recipes `cam.track`, `cam.sweep`, `cam.heroLow`, `cam.streetOverview`
  and the `moveBetween()` locomotion helper
- `<VillageStreet>` multi-angle street set, `CitizenLead` variants, `MoneyPrinter`
- `direction-report.mjs` hard gates for wall-spam, lazy cameras and static staging
- `SMALL-MODEL-CHEATSHEET.md` and `docs/REMASTER-V5-REFERENCE-STANDARD.md`
- Kept v4's `0.42s` TTS gap and the corrected clean-walk direction-test target

## Remaster v7 (final)

- `AGENTS.md` restored to the original storytelling-first director's contract:
  `MASTERPROMPT-01.md` first, seven-beat spine, story readable with the sound off,
  "stage the verb, then place the lens"
- New engine layer: `src/engine/collision.tsx` (actor pushback, `SolidBox` camera
  anti-clip) and `src/engine/Hud.tsx` (screen-space chat, clock, banner, subscribe)
- `cam.fitDist9x16()` and `cam.frameDuo()` for 9:16-safe two-shots; richer
  `press`/`fall`/`wave`/`hug`/`cheer` poses; camera-facing billboards
- ServerLore starter no longer draws a scoreboard
- Kept v4 TTS/BGM levels and the v5 direction hard gates

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
