# raiku-simulator task tracker

## IN PROGRESS

### Task 5 — Revenue flow: Other non-Raiku JIT
Status: IN PROGRESS
Last updated: 2026-03-22

Implemented so far:
- Other non-Raiku JIT is a derived read-only value: `max(Raiku Stake % - Raiku JIT Share, 0)`
- No free slider — updates live as stake or JIT share changes
- Source cards: Other JIT in separate left bypass column, Raiku gross trio to the right
- Distribution cards: "Validator Other JIT" left-most separate, Raiku dist cards to the right
- Flow diagram: Other JIT at top-left, Other JIT Validators at top-right, bypass arc above center node
- Methodology note updated to describe auto-derivation

Still pending (acceptance criteria not yet confirmed as satisfied):
- Visual review of card layout at different viewport sizes
- Confirmation of flow diagram geometry under live param changes
- Sign-off from user on all 12 acceptance criteria

---

## DONE

---

## BACKLOG

### Task 6 — (to be defined in next session)

---

## Session notes

2026-03-22 — Task 5 first pass: added Other JIT as free slider, separate flow paths, renamed labels.
2026-03-22 — Task 5 corrections: converted to derived value, reordered cards and SVG, removed double-count guard.
