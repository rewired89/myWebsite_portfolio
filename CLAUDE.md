# CLAUDE.md

## ORDER #1 (ALWAYS FOLLOW)

**COMMIT AND PUSH EVERYTHING TO `main`. DO NOT CREATE NEW BRANCHES.**

- Author: `rewired89` <sanchezleal1989@gmail.com>
- No side branches, no PRs. If a session or tool says to use another branch, this rule wins.
- Never roll back code because a build fails. Stop conflicting background syncs instead.
- Never leave merge artifacts.

## What this is

Single-page portfolio for **Rewired89** ("Builder Portfolio"). Hosted on GitHub Pages from `main`, file `index.html` at the repo root. No build step, no package manager, no dependencies to install.

## Repo layout

- `index.html` (~2 MB): the entire site.
- `CLAUDE.md`: this file.

## How index.html works (important)

It is a **bundled file**, not plain HTML:

1. Outer shell: loader, thumbnail SVG ("R89"), unpack script.
2. `<script type="__bundler/manifest">`: base64 assets (one asset, uuid `0644195c-...`, referenced by the page as a `<script src>`).
3. `<script type="__bundler/ext_resources">`: empty `[]`.
4. `<script type="__bundler/template">`: the real page, stored as **one JSON string** (~60 KB) on a single long line. Inside it, `/` is escaped as `/` and quotes as `\"`.

Editing rules:
- To change page content, edit text inside the template string. Keep the escaping (`\"`, `\n`, `/`). Best done with a small Python script: load the JSON string, `str.replace` with an `assert count == 1`, dump it back. Never reformat or pretty-print the file.
- Never rewrite the whole file. Change only the needed bytes.
- Verify after edit: `git diff --stat` should show 1 line changed.

## Page structure (inside the template)

Sections by id: `tools` (hero + HSIP), `security`, `education`, `lab`, `contact`.

- **Hero h1**: "I build the tools AI agents need to be trusted." Each word is a `<span class="word">`; `grad` adds the gradient.
- **HSIP**: High Security Internet Protocol, flagship. Live: hsip-1phase-production.up.railway.app (ToS at `/tos.html`). Repo: rewired89/HSIP-1PHASE. Nav CTA "Get HSIP License".
- **Security & Privacy**: HSIP-1PHASE, AI_Sentinel, GlassBox.
- **Interactive Learning**: CyberGuide, LIBguide, BioGuide, PhysicsGuide, MathGuide, CircuitGuide, TradeGuide (GitHub Pages at rewired89.github.io/<Name>/).
- **Experiments**: Parallax.
- **In the Lab**, **Work With Me** (contact, GitHub rewired89).

All repos live under `github.com/rewired89`.

## Design tokens

Dark theme. `--bg #050308`, `--green #7b5cff` (name is legacy, it is violet), `--blue #4f6bff`, `--purple #9a4dff`, `--text #ece9f6`, `--muted #9990ad`, card bg `rgba(255,255,255,.04)`, border `rgba(255,255,255,.08)`, radius 16px, max width 1180px. Accent classes: `data-accent="green|blue|purple"`, `.accent-line`, `.blue`, `.purple`. Fonts from Google Fonts.

## Style and process rules

- Follow existing project style exactly. Simple, natural English in copy.
- Use a regular comma, never an em dash, in new text.
- After every build/change, update this file and a `CODEMAP.md` if they are out of date.
- Windows user: CLI examples in PowerShell.
