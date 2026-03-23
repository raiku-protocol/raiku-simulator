# raiku-simulator task tracker

## IN PROGRESS

### Task 5 — Revenue flow: Other non-Raiku JIT
Status: IN PROGRESS
Last updated: 2026-03-23

Implemented so far:
- Other non-Raiku JIT is a derived read-only value: `max(Raiku Stake % - Raiku JIT Share, 0)`
- No free slider — updates live as stake or JIT share changes
- Source cards: Other JIT in separate left "Direct to validators" column, Raiku gross trio to the right
- Distribution cards: "Validator Other JIT" left-most separate, Raiku dist cards to the right
- Flow diagram: Other JIT at top-left, label above bypass arc, bypass arc above center node
- "Direct to validators" / "outside protocol take" wording throughout

Still pending:
- Consistent validator naming on right side: `Validator Other JIT`, `Validator Base`, `Validator AOT Bonus`
- Clean visual grouping of those three validator outputs on right side of flow diagram
- `Total Validator Revenue` far-right callout (sum of the three validator outputs only)
- Left `Other JIT` source label spacing/alignment polish
- Sign-off from user on all acceptance criteria

---

## DONE

---

## BACKLOG

### Task 6 — (to be defined in next session)

---

## Session notes

2026-03-22 — Task 5 first pass: added Other JIT as free slider, separate flow paths, renamed labels.
2026-03-22 — Task 5 corrections: converted to derived value, reordered cards and SVG, removed double-count guard.
2026-03-22 — Task 5 final: fixed label overlap (ojY svgTop+28, labels above arc), replaced "bypass" wording with "Direct to validators" / "outside protocol take".
2026-03-23 — Task 5 re-opened: naming consistency, validator total callout, left label polish still needed.
