# weekly-report

A Claude Code skill: a Monday memo for a site with Google Analytics 4 and
Search Console connected. It reads both, compares the week with the one
before, publishes a one-page report, saves it in the repo, and proposes
one to three actions. It opens a GitHub issue for an action only after you
say yes to it. It never writes pages, never changes anything in Google, and
never sends email.

## Install

```sh
git clone https://github.com/senblet/weekly-report ~/.claude/skills/weekly-report
```

Restart Claude Code. The skill shows up as `/weekly-report`.

## Needs

- Claude Code with Google Analytics 4 read access (the `analytics` MCP or a
  treg `google-analytics` connection) and Search Console read access (treg's
  `google-search-console`).
- The GA4 property id and the Search Console property of the site. The
  first run asks and saves them to `docs/weekly/config.json`.
- Optional: `gh` signed in, for issues; a git repository, for the history.

## Run

In the project's folder:

```
/weekly-report
```

or in words: "weekly report", "reporte semanal", "how did last week go".
Name a week to report another one.

What comes back: one verdict line and a link to the report. Then one
question per proposed action: open an issue, skip, or change the wording.

## What it applies

The rules are in [references/rules.md](references/rules.md): Search Console
as the source of truth, "too little data" said out loud, fix existing pages
before writing new ones (repoint pages at positions 5–15, cannibalisation
check, information-gain sentence, cadence cap on a new domain), links before
pages when Google crawls but does not index, AI referrals reported where
they appear and never as a score. They are distilled from
[senblet/Brain](https://github.com/senblet/Brain) (`seo/`, `marketing/`,
`ai/agents.md`).

## Files

- `SKILL.md`: the skill, phase by phase.
- `references/rules.md`: how numbers are read and actions chosen.
- `references/report-template.md`: the report's shape.
- `evals/`: prompts and expected behaviour, run by hand when the skill
  changes.

MIT.
