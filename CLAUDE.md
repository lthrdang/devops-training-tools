# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A DevOps & Cloud team onboarding system — self-contained HTML apps + Markdown docs that take a new team member from pre-assessment through a 10-day story-driven training to a final capstone evaluation. No build system, no server, no dependencies.

## Architecture

All HTML files are **single-file apps** (HTML + CSS + JS inlined). They use browser-native APIs only — no frameworks, no bundler. State is persisted via `localStorage` and JSON file import/export.

The site is split into **two separate static surfaces** sharing the same origin:
- Root (`/`): trainee-facing — `index.html` + the pre-test and story training apps
- `trainer/`: trainer-only console — `trainer/index.html` + dashboard and assessment rubric

The split is physical (separate directories), not access-controlled. Anyone with the URL can reach `trainer/`; the goal is UI separation, not security.

**Data flow between tools:**
- The **pre-test** (`devops-pretest.html`) generates a JSON progress file with scores and per-section recommendations (full/skim/skip)
- The **story training** (`ecotrack-story-training.html`) loads that JSON, tracks chapter completion, and re-exports the updated file
- The **trainer dashboard** (`trainer/dashboard.html`) reads the `progress/` folder (via File System Access API — user picks the folder, no hardcoded path) to display a cohort overview
- The **assessment rubric** (`trainer/assessment-rubric.html`) is filled by the trainer at Day 10; scores auto-calculate and state saves in `localStorage` under the key `ecotrack-rubric`

Progress files live in `progress/` as flat JSON — one file per trainee, git-tracked. Schema is defined in `progress/_template.json`.

## Conventions

- Dark theme with CSS custom properties (shared `--bg`, `--surface`, `--accent`, etc. palette across all HTML files)
- All HTML files are designed to be opened directly in a browser (`file://` or any static server) — no build step
- Print-friendly CSS via `@media print` overrides (assessment rubric)
- The roadmap (`devops-cloud-onboarding-roadmap.md`) is pure Markdown, used as a reference doc alongside the story training

## When Editing

- Keep each HTML file fully self-contained — do not extract CSS/JS into separate files
- Maintain the shared CSS custom property naming convention across files
- The progress JSON schema (`_template.json`) is the contract between the pre-test, story training, dashboard, and assessment tools — changes must stay backward-compatible
- Test HTML changes by opening the file directly in a browser
