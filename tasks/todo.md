# raiku-simulator task tracker

## IN PROGRESS

---

## DONE

### Task 5 — Revenue flow: Other non-Raiku JIT
Status: DONE
Last updated: 2026-03-23

Implemented:
- Other non-Raiku JIT is a derived read-only value: `max(Raiku Stake % - Raiku JIT Share, 0)`
- No free slider — updates live as stake or JIT share changes
- Source cards: Other JIT in separate left "Direct to validators" column, Raiku gross trio to the right
- Distribution cards: "Validator Other JIT" left-most separate, Raiku dist cards to the right
- Flow diagram: Other JIT at top-left, label above bypass arc, bypass arc above center node
- "Direct to validators" / "outside protocol take" wording throughout
- Consistent validator naming: `Validator Other JIT`, `Validator Base`, `Validator AOT Bonus`
- Validator total brace opens LEFT toward outputs, pointer to callout at x=952
- `Total Validator Revenue` shows `$X (Y%)` — same format as other flow outputs
- `Validator Base` 3-line block: label / `(Raiku JIT + AOT)` / `$X (Y%)` — 16px gaps, no overlap
- Left sources: `Other JIT Revenue`, `Raiku JIT Revenue`, `AOT Revenue`
- Right side top aligned with left side top: `rightTop = svgTop+28`, `availH = svgH-rightTop-svgTop-totalGapH`
- Right side vertical span matches left source stack span (top-to-bottom alignment)
- viewBox: 0 0 1060 540, svgH=520, barGap=12, minBarH=30

---

### Task 5.bis — Add 3.5L fee/CU bucket to AOT sensitivity chart and table
Status: DONE
Last updated: 2026-03-23

Implemented:
- Added `3.50` between `2.00` and `5.00` in the `fc` array inside `buildMatrix()`
- `fc` is now: `[0.10, 0.20, 0.50, 1.00, 1.50, 2.00, 3.50, 5.00, 10.00, 20.00]`
- Label format `f.toFixed(1)` renders it as `3.5L` automatically
- `nearestIdx(fc, p.f)` now resolves to the `3.5L` bucket when Bull Case is active
- No change to revenue flow logic, validator splits, or any other tab

---

## BACKLOG

### Task 6 — Annual Revenue Overview update
Status: DONE (implemented separately)

### Task 7 — Validator Revenue logic cleanup
Status: DONE
Last updated: 2026-03-23

Implemented:
- Epoch-based compounding: `EPOCHS_PER_YEAR = Math.round(SY / 432_000)` ≈ 182; `APY_COMPOUNDING_PERIODS` now uses this constant instead of 365
- Added "Other JIT (direct)" KPI card in Validator Revenue Pool (color #6B9EBC)
- Renamed "JIT Validator Revenue" → "Raiku JIT" (color #5B8DEF), "AOT Validator Revenue" → "AOT Base", "AOT Validator Bonus" → "AOT Bonus" (color #4178DE); Total visually bold
- `totalValidatorRevenueSol = r.totalValRev + r.otherJitRev` — all 4 components included
- `renderValidatorYieldScenarioComparison` APR calc also includes `r.otherJitRev`
- All "daily compounding" static text strings updated to "epoch-based compounding"
- Formula note updated: lists all 4 components + epoch-based convention

---

## Session notes

2026-03-22 — Task 5 first pass: added Other JIT as free slider, separate flow paths, renamed labels.
2026-03-22 — Task 5 corrections: converted to derived value, reordered cards and SVG, removed double-count guard.
2026-03-22 — Task 5 final: fixed label overlap (ojY svgTop+28, labels above arc), wording polish.
2026-03-23 — Task 5 polish: validator naming, brace callout, left label naming and spacing.
2026-03-23 — Task 5 brace fix: viewBox 1060, brace x=930, percentage line, source label "Revenue" suffix.
2026-03-23 — Task 5 brace direction: reversed brace to open left, $X (Y%) format, Validator Base sub-label.
2026-03-23 — Task 5 spacing: viewBox 540 tall, svgH=520, barGap=12, minBarH=30.
2026-03-23 — Task 5 alignment: rightTop=svgTop+28 aligns right stack top with left stack; Validator Base 3-line block with parens and clear gaps.
2026-03-23 — Task 5 sign-off. Task 5.bis: added 3.5L bucket to sensitivity table fc array.
