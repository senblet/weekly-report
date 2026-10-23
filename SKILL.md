---
name: weekly-report
description: Weekly traffic and search report for a site with Google Analytics 4 and Search Console connected. Use when the user says "weekly report", "reporte semanal", "how did last week go", "come è andata la settimana", "/weekly-report", or asks what to do next about SEO or traffic. Reads GA4 and Search Console (never edits them), compares the week with the one before and with the saved history, publishes a one-page report as an artifact, saves it in the repo, and proposes 1–3 actions; it opens a GitHub issue for an action only after the user says yes to that action. It never writes pages, never publishes content and never sends email.
---

# Weekly report

A Monday memo for one site: what moved, why if known, and what to do this week.
Every line ends in keep, improve, write, wait or ask.

It applies the studio's Brain (`seo/`, `marketing/conversion.md`,
`marketing/agents.md`, `ai/agents.md`). The rules the report applies are in
[references/rules.md](references/rules.md); read it before writing the actions.

## Requirements

Hard. If one is missing, say which and stop:

- **GA4 read access** in this session: the `analytics` MCP
  (`run_report`, `get_account_summaries`) or treg's `google-analytics`
  connection.
- **Search Console read access**: treg's `google-search-console` connection
  (`performance`, `url_inspection`, `sitemaps`).
- **The project's identifiers**: GA4 property id and Search Console property
  (`sc-domain:example.com` or `https://example.com/`). Look in the project's
  `AGENTS.md`/`CLAUDE.md`, `docs/weekly/config.json` and
  `utils/analytics.ts`; otherwise list the accounts and ask once, then
  write them to `docs/weekly/config.json` so the next run does not ask.

Soft. Continue without them and say so in the report:

- `gh` signed in, for issues. Without it, list the actions without links.
- A git repository, for saving the report. Without it, the artifact is the
  only copy.
- The project's own context (`AGENTS.md`, `docs/seo/`, a keywords folder, a
  guides folder). Read what exists: the actions must follow the project's
  rules, not only the Brain's.

## Phase 0: scope

1. **Week.** Default: the last full Monday–Sunday. Search Console lags about
   two days, so if the run is before Wednesday, say the last two days may
   still rise. The user may name another week.
2. **Previous report.** Read `docs/weekly/` for the newest `YYYY-MM-DD.md`
   and `log.md`. The report compares with the previous week's numbers and
   says whether an earlier action was done (issue closed, page changed).
3. **Project context.** Read `AGENTS.md`/`CLAUDE.md` and `docs/seo/overview.md`
   if present; note publishing rules (bylines, sources, cadence, what is
   `noindex`), the list of public pages, and open GitHub issues
   (`gh issue list --state open`), so no action duplicates one.

## Phase 1: pull the data

Read only. Pull both weeks in one call each.

**GA4** (`run_report` with two date ranges, this week and the one before):

- Sessions, total users, new users, engaged sessions by
  `sessionDefaultChannelGroup`.
- Product events: the project's conversion names (GA4's `sign_up` plus the
  allowlist in the project's analytics module). Count per event.
- Top pages by `screenPageViews`.
- `sessionSource` / `sessionCampaignName` for this week, to attribute social
  posts and campaigns; `utm_source=chatgpt.com` and other assistant sources
  count as AI referrals.

**Search Console** (`google-search-console.performance`, `dataState: all`):

- Site totals for this week and the week before: clicks, impressions,
  position.
- Queries and pages for the last 28 days (7 days is too thin on a small
  site), `rowLimit` 100.
- `sitemaps`: when Google last read the sitemap and how many URLs it holds.
- Index state: inspect every sitemap URL with `url_inspection` when there
  are 50 or fewer (one call each, free, 2,000/day). Above that, inspect the
  pages that changed since the last run plus a sample of 20. Count
  "indexed", "crawled, not indexed", "discovered, not crawled", "unknown".

Record what failed ("Search Console returned nothing for the week") instead
of skipping it silently.

## Phase 2: read the numbers

Small sites have small numbers. Say "too little data" when it is true; do
not invent a trend from 5 visits. Rules, in [references/rules.md](references/rules.md):

- What counts as a change worth a sentence (thresholds).
- Which pages to repoint (positions 5–15, not edited in the last 60 days).
- When a query justifies a new page (cannibalisation check first,
  information-gain sentence, cadence cap).
- What the report cannot see (pages without analytics, manual AI checks).

Write one verdict line first, then the sections.

## Phase 3: the report

Build the page from [references/report-template.md](references/report-template.md)
and publish it as an artifact (load the `artifact-design` skill first; keep
the same file path across weeks so the URL stays stable, or the `url` of the
previous week's artifact when it is recorded in `log.md`). Language: the
project's user-facing language (Spanish for a Chilean site; the Brain is
English, the report is for the owner).

Save the same content as Markdown at `docs/weekly/YYYY-MM-DD.md` (the Monday
of the reported week), commit it with the project's commit conventions, and
push only if the project's rules allow pushing without asking.

Sections, in order:

1. **Verdict**: one sentence.
2. **Visits**: four numbers with deltas, sources, product events.
3. **Search**: impressions, clicks, indexed pages (n / total in sitemap),
   top pages with position, visible queries.
4. **What to do this week**: 1–3 actions ranked, each with the data behind
   it and a "why now". Include a "do not do X yet" line when the data says
   so. Mark each as new, or carried from a previous week with its issue.
5. **What this report cannot see.**
6. **Footer**: date generated, sources, link to the previous report.

## Phase 4: actions, one yes at a time

For each action that has no open issue, ask the user with one question per
action: open an issue, skip, or edit the wording. Never open an issue
without a yes. For a yes, create it with `gh issue create`, body in the
project's language with the data and the Brain rule it follows, and add the
link to the report (republish the artifact and amend the Markdown).

An action that already has an issue gets a link, no question.

## Phase 5: log

Append one line to `docs/weekly/log.md`:
`YYYY-MM-DD | week YYYY-MM-DD..YYYY-MM-DD | sessions N (±N) | clicks N | indexed N/N | actions: #12 new, #4 carried | artifact URL`.
Commit it with the report. Reply with the verdict and the artifact link,
nothing else.

## Rules that never break

- Read-only on GA4, Search Console and the site. The skill never requests
  indexing, never edits robots.txt, canonicals or the sitemap, never
  publishes content, never sends mail.
- Issues only after an explicit yes, one per action.
- No personal data in the report or the log: aggregate numbers only, never
  user ids, emails or full URLs that carry tokens.
- A missing source is reported, not papered over.
- The report says what it cannot see.
