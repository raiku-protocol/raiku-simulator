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
- Consistent validator naming: `Validator Other JIT`, `Validator Base`, `Validator AOT Bonus`
- Validator total brace on right side, clear of labels (viewBox extended to 1060, brace at x=930)
- `Total Validator Revenue` callout with value + percentage of distributed revenue
- Left sources labeled consistently: `Other JIT Revenue`, `Raiku JIT Revenue`, `AOT Revenue`
- Left Other JIT spacing: 20px gap (matches Raiku JIT / AOT treatment)

Still pending:
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
2026-03-23 — Task 5 polish: validator naming consistency, total validator brace callout, left label naming + spacing.
2026-03-23 — Task 5 brace fix: extended viewBox to 1060, pushed brace to x=930, added percentage line, left source labels renamed with "Revenue" suffix.
