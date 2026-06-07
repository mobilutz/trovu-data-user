# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A data-only repository for [trovu.net](https://trovu.net) — a web shortcut launcher. It contains personal user configuration and shortcut definitions, consumed by trovu.net via the GitHub namespace mechanism described at https://trovu.net/docs/users/advanced/.

There is **no build, no test suite, and no application code** in this repo. Changes are pushed to `master` and picked up by trovu.net directly.

## Files

- `config.yml` — user-level config: `namespaces` (which shortcut namespaces to load, including this repo aliased as `.`), `defaultKeyword`, `language`, `country`. See https://trovu.net/docs/users/advanced/#custom-configuration.
- `shortcuts.yml` — the user's personal shortcuts. Keys use the form `<keyword> <argument-count>` (e.g. `gmail 0`, `yt 1`, `db< 1`). Each entry has a `url` and usually a `title`. Argument placeholders inside `url`:
  - `{%name}` — free-text argument.
  - `<name: {type: city}>` — typed argument (city, date, time, etc.).
  - `{$language}`, `{$country}` — user config values.
  - `<$now: {output: YYYY-MM-DD}>` — dynamic value.
  - `#trovu[waitBeforeFill]=…&trovu[submit]=…` — trovu post-load actions (fill delay, auto-submit selector).

## Editing notes

- Shortcut keys must match the `keyword count` pattern; `count` is the number of arguments referenced in the URL.
- Validate by loading the shortcut on trovu.net after pushing — there is no local linter.
- Keep `config.yml` `namespaces` list aligned with the trovu namespaces the user actually wants loaded; `github: .` means "this repo's shortcuts.yml."
