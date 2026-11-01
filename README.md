# kb — the support knowledge base

**kb** = knowledge base. What the support desk knows about how our products break, written
down where the code can keep it honest.

One desk takes reports for every product we run: `sched-prod` (calendar invites for about
300k people) and the rest. When something
goes wrong, the reports reach the desk first. This kb is how the desk triages them, what each
incident turned out to be, and why we decided what we decided.

## What's here

```
src/routes/kb/      the pages (.svx: Markdown with components)
  triage/           how the desk handles incoming reports
  incidents/        one page per big ticket
  decisions/        numbered decision records
src/lib/kb/         components and the logic they run
src/lib/layouts/    the frame every page shares
src/lib/data/       exports from the ticket system
```

## Conventions

- Words in the page, logic in `src/lib` (imported as `#lib/…`). A number that can be computed belongs in a component.
- Every page starts with frontmatter: `title`, `owner`, `status`, `reviewed`.
- A decision is never edited after it is accepted. A new record replaces it.
- A page you add is signed: its frontmatter carries your `signature` and it ends with `<RenderStamp {signature} />`, so the desk knows who wrote it.

## Owners

Support desk. Decision records: whoever signed them.

## Challenge review: #4471

- [Signed split page](src/routes/kb/incidents/4471-split/+page.svx)
- [Rendered page preview](preview/4471-split.html)
- [Parser issue: 379 reports](https://github.com/mkuczera/mega-s01e03-what-it-shows/issues/1)
- [Booking-v3 hint issue: 33 reports](https://github.com/mkuczera/mega-s01e03-what-it-shows/issues/2)

The page reads the exported reports through `src/lib/kb/Split4471.svelte`; its counts are computed after deduplicating report IDs. The preview shows the same export as of 2026-10-04.

---

Exported 2026-10-04 from the `support` repo, `apps/kb/` → `src/`.
