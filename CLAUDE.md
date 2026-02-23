# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Wiki.js content repository** for school notes on two subjects:
- **Informatik** (Programmiertechnik) — algorithms, data structures, programming languages, paradigms
- **IT-Labor** — Java, Git, Docker, dev environments

The Markdown files sync directly to a self-hosted Wiki.js instance via Git — no build step. This is a living wiki that grows continuously: new pages, new subjects, and updates to existing content will be added regularly as the school year progresses.

## File Structure

```
home.md                    — Navigation hub
informatik/                — Informatik subject
it-labor/                  — IT-Labor subject
assets/images/             — Images referenced in pages
notizen.org                — Original Org-mode source notes (gitignored)
```

## Content Philosophy

Every page should be:
- **Praxisnah** — grounded in what we actually do and need at school, not theoretical overviews
- **Präzise** — straight to the point, no filler, no padding
- **Korrekt** — technically accurate; when in doubt, leave it out rather than guess
- **Auf Deutsch** — all content in German, including headings and explanations (code and technical terms stay in English)

## Page Format

Every page starts with Wiki.js frontmatter:

```yaml
---
title: page-slug
description:
published: 1
date: 2026-02-21T10:53:58.440Z
tags:
editor: markdown
dateCreated: 2026-02-21T07:24:43.060Z
---
```

Slug style: lowercase kebab-case (`/it-labor/git-grundlagen`).

## Filling Gaps

If the notes on a topic are incomplete:
- **Fill inline** if the missing content is ≤ 1–2 paragraphs, or if explicitly asked (e.g. `git pull - explain`)
- **Skip** everything else — leave it out rather than pad the page

## Diagrams

Mermaid diagrams use the `kroki` code block syntax (not plain `mermaid`):

````
```kroki
mermaid

%%{init: {'theme': 'base', 'themeVariables': {'background': '#231f20', 'mainBkg': '#3b9689', 'primaryColor': '#3b9689', 'primaryTextColor': '#fff', 'primaryBorderColor': '#70c7ba', 'lineColor': '#70c7ba', 'edgeLabelBackground': '#282425', 'nodeTextColor': '#fff', 'clusterBkg': '#282425'}}}%%
graph TD
    ...
```
````

The `mermaid` keyword must be on its own second line. Always include the `%%{init: ...}%%` dark-theme block for visual consistency.

**Diagram tool choice:**
- **Mermaid** (via Kroki) — flowcharts, mindmaps, sequence diagrams (current default)
- **PlantUML** — use when OOP class diagrams with inheritance/interfaces are needed (Mermaid class diagrams are too limited for that)
