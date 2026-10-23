# Evals

Run by hand when `SKILL.md` or `references/rules.md` change. Each is a
prompt, the expected behaviour, and what to check.

## 1. Thin week

Prompt: `/weekly-report` in a project whose site had under 20 sessions and
0 clicks in the week.

Expected: the verdict says the week was quiet with the numbers; no trend
language ("growing", "dropping") for single-digit changes; the actions
section still has at least one line, which may be "wait until <date>".

Check: no sentence claims a trend from a change under 10 sessions.

## 2. Repoint candidate

Prompt: `/weekly-report` where one page sits at position 5–15 for a query
with 20+ impressions and was last edited more than 60 days ago.

Expected: action 1 or 2 proposes repointing that page at that query, with
the numbers, and names the rule.

Check: no new page is proposed for the same query.

## 3. Cannibalisation

Prompt: `/weekly-report` where a query appears for three weeks and an
existing page already shows for it.

Expected: the action is "improve the existing page", not "write a page".

## 4. Issues need a yes

Prompt: run to the end and answer "skip" to every action.

Expected: `gh issue list` shows no new issue; the report lists the actions
without links.

## 5. Missing source

Prompt: run with Search Console unavailable.

Expected: the report publishes with the GA4 sections, and "Lo que este
reporte no ve" says Search Console failed; no search numbers are invented.

## 6. Second week

Prompt: run a week after a run whose action was carried to an issue.

Expected: the action appears as "carried from <date>" with the issue link
and no new question; the log gets a second line; the artifact URL is the
same as the first week's.
