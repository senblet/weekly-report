# Report template

The same content ships twice: as an artifact page and as Markdown in
`docs/weekly/YYYY-MM-DD.md`. The Markdown version is the one below; the page
follows the same order with the numbers as tiles and the deltas as chips.
Replace every `<…>`; drop a section only when its source failed, and say so
in "What this report cannot see".

Language: the project's user-facing language. Dates absolute and ISO in the
Markdown; the page may spell them out.

```markdown
# <Site> · semana <YYYY-MM-DD> a <YYYY-MM-DD>

**<One-sentence verdict: the single most important thing that happened, with a number.>**

Comparado con la semana anterior (<dates>). <Lag note if the run is before Wednesday.>

## Visitas (GA4)

| | Esta semana | Anterior | Cambio |
|---|---|---|---|
| Sesiones | N | N | ±N |
| Visitantes nuevos | N | N | ±N |
| Sesiones con interacción | N | N | ±N |
| <Main conversion event, e.g. ventas empezadas> | N | N | ±N |

De dónde vinieron: <sources and campaigns in one sentence; AI referrals named if any>.

## Búsquedas (Search Console)

| | Esta semana | Anterior |
|---|---|---|
| Impresiones | N | N |
| Clics | N | N |
| Posición media | N | N |
| Páginas indexadas | N / <sitemap total> | N / <total> |

Páginas con más impresiones (28 días):

| Página | Impresiones | Clics | Posición |
|---|---|---|---|
| … | | | |

Búsquedas visibles (28 días): <list with impressions; say how many Google withholds>.

Estado del índice: <n indexed, n crawled-not-indexed, n discovered, n unknown; sitemap last read on <date> with <n> URLs>.

## Qué hacer esta semana

1. **<Action>.** <Data behind it. Rule it follows. New / carried from <date>.> <Issue link or "sin issue todavía">
2. …
3. …

<"No hacer todavía: …" line when applicable.>

## Lo que este reporte no ve

<Pages without analytics (private links), manual checks (AI citations, due <date>), backend counts, sources that failed this run.>

---

Generado el <date> desde GA4 (<property id>) y Search Console (<property>). Reporte anterior: <link or "ninguno">.
```

Page notes (artifact):

- Verdict as the heading. Tiles for the four GA4 numbers and the three search
  numbers, each with a delta chip (up / down / flat in semantic colours,
  separate from the accent).
- Tables in `overflow-x: auto`. Tabular numerals.
- Actions as an ordered list because they are ranked; each with the reason
  in a muted line and the issue link in mono.
- One quiet accent; no hero, no decoration. It is a memo.
- Both themes, phone width, no horizontal scroll.
