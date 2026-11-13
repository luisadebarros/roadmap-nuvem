# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Interactive cloud-study roadmap (UI text in Brazilian Portuguese) with three tabs: **Microsoft Learn**, **AWS** and **Docker & Kubernetes**. Each item links to an official study page and has a checkbox; progress is saved in `localStorage`, separately per tab.

The whole app is a single file, `index.html`: plain HTML/CSS/JS with no dependencies, build step, linter or tests. To run it, open `index.html` in a browser.

## Architecture of `index.html`

- **Content**: one IIFE per tab (`MS`, `AWS`, `K8S`), each returning `{TOOLS, STOPS}`. Most edits happen here.
  - `TOOLS`: `{t, d, url}`. These are the links in the "Ferramentas" section.
  - `STOPS`: the ordered route. A normal stop is `{id, title, blurb?, groups:[{label, items:[...]}], cert?, cols?, wide?}`. A stop with `milestone: true` (plus `title`, `cert`, `next`) is the certification "bloom". It splits the map into its "before" and "after" sections and only blooms once every earlier stop is complete.
  - Item: `{t, k, url, note?}` where `k` is one of `trilha | modulo | docs | video | pratica | cert` (labels in `KIND`).
  - URL prefixes are local constants in each block, e.g. `L` (MS Learn pt-br), `D` (AWS docs pt_br), `SB` (Skill Builder), `DK` (Docker docs), `K` (kubernetes.io docs).
- **`TABS`**: per-tab config that spreads in the content block plus the header and footer copy and the `localStorage` key (`roadmap-mslearn-luisa-v1`, `roadmap-aws-luisa-v1`, `roadmap-k8s-luisa-v1`). Page titles live in `TITLES`. The active tab is stored under `roadmap-tab-luisa`.
- **Adding a tab** takes a content IIFE, a `TABS` entry, a `TITLES` entry and a `data-tab` button in the `.tabs` markup. Arrow-key navigation cycles through `Object.keys(TABS)`.
- **Rendering**: `loadTab()` swaps the globals `STOPS`/`TOOLS`/`KEY`/`state`. `render()` builds the stops, the map and the tools as HTML strings (always pass content through `esc()`). `sync()` applies the checkbox state, counts, progress bars and the current-stop/milestone classes. `placeMarker()` positions the flower on the route.

## Gotchas

- **Progress is keyed by `stop.id + '/' + slug(item.t)`**. Renaming an item's title, or changing a stop `id`, silently drops users' saved checks for that item. Bump the storage key only if a reset is intended.
- Theming uses CSS tokens on `:root`, with dark mode defined both under `prefers-color-scheme` and under `[data-theme="dark"]`. Add new colors as tokens in both places.
- Animations respect `prefers-reduced-motion` (the `reduce` flag in JS).
