# Rules the report applies

Distilled from the studio's Brain (`seo/overview.md`, `seo/content.md`,
`seo/ai-search.md`, `seo/links.md`, `marketing/conversion.md`,
`marketing/agents.md`, `ai/agents.md`; read 2026-10-23). The Brain wins when
the two disagree; a project's own `AGENTS.md` wins over both.

## Reading the numbers

- **Search Console is the source of truth for search.** GA4 counts visits;
  Search Console counts what Google showed. Never derive one from the other.
- **Search Console data lags about two days**, and rows under Google's
  privacy threshold are withheld, so the sum of queries never equals the
  site total. Use site totals for the headline and query rows for the
  reasons.
- **Compare like with like**: this week against the week before, same seven
  days. For queries and pages use 28 days; a week is too thin on a small site.
- **Say "too little data" when it is true.** Under about 100 sessions a week,
  a change of a few visits is noise. Report it as a number with a plain
  sentence, not as a trend.
- **A change worth a sentence**: sessions or impressions move by 30% or more
  and by at least 10; a page enters or leaves the top 10; a query gains 10 or
  more impressions; the indexed count changes; a conversion event moves at
  all when it is under 10 a week.
- **Conversions come from one source of truth** (the backend, the backoffice
  count), never added up across platforms. Report GA4 events as "GA4 saw",
  not as the real count, when the project has a backend count.
- **Attribution is a cross-check, not credit.** Campaign and source rows say
  where a visit came from; they do not say what caused a sign-up.
- **AI referrals** show as `utm_source=chatgpt.com` and similar sources in
  GA4, and AI Overviews are counted inside the "Web" search type in Search
  Console, not separately. Report them where they appear; never report an "AI
  visibility" score. The monthly manual check (about 10 buyer questions, each
  asked 3–5 times, logged out, recorded as cited / mentioned / recommended /
  recommended against, with its sample "3/5") is done by a person; the
  report says when it is due and links the last one if the project keeps it.

## Index state

- A page is only eligible if it returns 200, is not blocked by robots.txt
  and has indexable content. Any page failing one of those is a bug: name
  it, with its fix.
- "Crawled, currently not indexed" and "Discovered, currently not indexed"
  are not errors. On a new domain they mean few links from other sites and a
  burst of pages. The fix is links and time, not settings. Never propose
  resubmitting the sitemap when Google read it after the last change.
- Requesting indexing is a manual step in Search Console; the report may
  suggest it for 2–3 priority pages, never for all.
- Do not propose blocking AI crawlers; that is an owner decision, not an SEO
  fix. Do not propose `llms.txt` or special AI markup; Google says they do
  nothing.

## Choosing actions

Ranked order, from the Brain's "improve existing pages before publishing
more":

1. **Fix a bug** (a page that stopped returning 200, a lost canonical, a
   `noindex` that appeared, a sitemap error). Always first.
2. **Repoint a page**: a page at position 5–15 for a query with impressions,
   not edited in the last 60 days. Action: rewrite title, H1, meta
   description and first 100 words around that query; check the body
   answers it. At positions 1–3 with falling clicks, an AI summary is
   probably answering above it; a rewrite will not help, say so. Stop after
   two rounds of edits that moved nothing: the gap is authority.
3. **Links**: when most pages are "discovered / crawled, not indexed" and
   nothing technical is wrong, the action is earning links from sites in the
   niche (the project's outreach list if it has one). The Brain's method:
   collect what is already yours (unlinked mentions, lost links), ask only
   where the ask is reasonable, give before asking, a handful a day, never
   paid links without `rel="sponsored"`.
4. **Write a new page** only when all of these hold:
   - a query (or a pattern of queries) shows impressions for three weeks or
     more, or the owner's keyword research names it;
   - the cannibalisation check passes: no existing page already shows for
     that query (if one does, improve it instead);
   - one sentence says what the page adds that the top results lack
     (information gain); if the sentence cannot be written, do not propose
     the page;
   - the cadence cap holds: on a new domain, at most three or four pages a
     week, each one a person would read; the report counts what went out in
     the last 7 days and says how much room is left;
   - the project's own publishing rules are listed in the issue (byline,
     sources, no invented market facts, `dateModified`, sitemap).
   The report proposes the page; a person writes and checks it. The skill
   never writes it.
5. **Prune**: a page with no clicks and negligible impressions over 90 days,
   older than three months, that reads thin or wrong. Propose merge or
   delete on quality, never to lower the count.
6. **Wait**: when nothing above applies, say so and name the next date
   worth looking (two to three weeks for a new change; about two months
   before judging a title change; about six months before a new domain
   compounds).

Every action names the data behind it, the rule it follows, and whether it
is new or carried over. At most three. A "do not do X yet" line counts as
guidance, not as an action.

## What the skill never does

- Writes or edits a public page, a guide or the sitemap.
- Requests indexing, changes robots.txt, canonicals, redirects or DNS.
- Opens an issue without an explicit yes for that action.
- Sends email or any message.
- Puts personal data in the report: no user ids, emails, IPs, or URLs that
  carry tokens. Aggregates only.
- Hides a failed source. "Search Console returned nothing" is a line in
  the report.
