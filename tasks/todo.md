# raiku-simulator task tracker

## DONE

### Revenue Model follow-up — protocol take split and presentation cleanup
Status: DONE
Last updated: 2026-03-23

Implemented:
- Part A: Removed shared sl-gb; added sl-gb-aot (AOT, default 2.5%) and sl-gb-jit (JIT, default 2.5%) using % of gross grammar with pool-share helper text
- Part B: viewBox 0 0 1100 540; Treasury Pool color #9EBF6A (muted); old separator/label removed; fk-proto-brace + fk-proto-take-lbl/lbl2/v spanning outputs[2..6]
- Part C: Nested distribution cards — Other JIT separate left, Validator Base standalone, Protocol Take family column (summary card + 5 subcards grid: AOT Bonus, AOT Rebate, JIT Rebate, G+B, Treasury)
- calc(): separate aotGBRate/jitGBRate clamped to available pool; totalProtocol = treasury residual; totalProtocolTake + totalProtocolTakeUSD returned
- Commit: 6dedb30

---

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

### Task 8 — Revenue flow: denominator fix + Protocol Revenue rename + Growth+Buyback + visual grouping
Status: DONE
Last updated: 2026-03-23

Implemented:
- Right-side flow diagram bars use `r.totalGrossUSD` (Raiku gross) as denominator — not polluted by Other JIT bypass
- Other JIT bypass bar shows dollar value only, no percentage
- Total Validator Revenue brace callout shows dollar value only, no percentage
- Central node renamed from "Raiku Gross" → "Protocol Revenue"
- Added Growth + Buyback slider (`sl-gb`, 0–100% of protocol pool, default 0%)
- `calc()` splits `totalProtocol` into `growthBuyback` + `treasuryPool`
- New `fk-gb` bar in flow diagram (color #A0C878)
- `fk-proto-label` renamed to "Treasury Pool"
- `sl-gb` wired to event listener array and `gp()`
- Dynamic horizontal separator line (`fk-proto-group-sep`) between validator outputs and protocol-take allocation group
- "Protocol Take ▾" group label (`fk-proto-group-label`) positioned at separator by `updFlow()`
- `ratio-gb` pool-usage indicator under G+B slider: "N% of protocol pool → $X/yr" or "inactive (0%)"

Protocol-take reconciliation (cleanly verifiable):
  `jitGross × jitTakeRate + aotGross × aotTakeRate`
  `= AOT Rebate + JIT Rebate + Validator AOT Bonus + Growth+Buyback + Treasury Pool`

---

### Task 8.bis — Validator Revenue methodology
Status: DONE
Last updated: 2026-03-24

Implemented (methodology already in code, confirmed):
- `issuanceAPR = SOLANA_INFLATION_RATE / stakingRatio` (validator-level gross, no commission)
- `priorityFeesApr = PRIORITY_FEES_NETWORK_APR * residualBlockShare`
- `incrementalAprUplift = totalValidatorRevenueSol / connectedStakeSol`

---

### Validator Revenue redesign — Patch 1: decomposition bar expansion
Status: DONE
Last updated: 2026-03-24

Implemented:
- Part A: Expanded decomp bar from 3 segments to 6 segments (Issuance / Residual Block Fees / Raiku AOT / Validator Bonus / Raiku JIT / Other JIT)
- Part B: APY primary (large), APR secondary (small) in all 6 legend entries; Total row keeps `totalApy = aprToApy(totalApr, n)`
- Part C: New CSS colors — base #A0C878, priority #6B9EBC, aot #7BBBAF, bonus #4178DE, jit #5B8DEF, other-jit #8E77C7. Added `.validator-decomp-seg` and `.validator-decomp-dot` classes for all 4 new types.
- Part D: HTML decomp bar replaced (6 seg IDs: iss/blk/aot/bonus/jit/ojit); legend replaced (7 entries: 6 components + Total)
- Part E: `update()` wired — per-component APR vars `aotApr/bonusApr/jitApr/ojitApr` computed from `r.*`; bar widths and legend values set for all 6 segments. Old 3-seg lines removed.
- Part F: `renderValidatorYieldScenarioComparison` updated to 6-segment bars per scenario card; same APR decomp logic applied.
- bonus component uses `r.aotValBonus + (r.jitValBonus || 0)` (not `r.validatorBonus` which does not exist in calc())

---

### Validator Revenue redesign — Patch 2: protocol composition card
Status: DONE
Last updated: 2026-03-24

Implemented:
- New top composition card (vc-*): Total APY headline / Raiku APY Uplift / Total APR / 6-seg bar / 6 component rows
- 6 component rows: Issuance / Network Block Fees / Raiku AOT / Validator Bonus / Raiku JIT / Other JIT
- APY primary, APR secondary, SOL/yr per component row (uses existing fmtValidatorSol + '/yr')
- Old "Yield Uplift" 4-card block removed; section renamed "Yield Details"
- "Validator audit line" removed (redundant with top card)
- "Base Network Yield" sidebar section hidden; sl-staking-ratio slider kept in DOM as hidden input
- Hidden spans preserve all IDs still written to by update(): validator-uplift-apy/apr, validator-total-apy/apr, validator-apr-formula-line/note, validator-apy-formula, validator-staked-value/source, validator-inflation-rate, validator-staking-ratio-display, validator-base-apr/sub/apy, validator-priority-apr/apy
- CSS: added .vc-row, .vc-row-left, .vc-row-name, .vc-row-right, .vc-row-apy, .vc-row-apr, .vc-row-sol
- No math changed; all values from existing update() computation (issApy2/blkApy2/aotApy2/bonusApy2/jitApy2/ojitApy2 to avoid name collision with aprToApy calls already in scope)

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
2026-03-23 — Task 8: denominator fix, Protocol Revenue rename, Growth+Buyback allocation. Commit 26721dd.
2026-03-24 — Patch 1: 6-segment decomp bar expansion, APY primary/APR secondary, 6 new colors.
2026-03-24 — Patch 2: top composition card, removed Yield Uplift 4-cards + audit line, hidden Base Network Yield sidebar.
