---
title: Functional Completeness
type: concept
tags: [logic-gates, boolean-algebra]
sources: [raw/summaries/ti_1.pdf]
created: 2026-10-25
updated: 2026-10-25
---

## Summary

A set of logic gates is **functionally complete** if any Boolean function
can be built using only gates from that set. NAND alone is functionally
complete, and so is NOR alone — this is why real hardware is often built
from a single gate type for manufacturing simplicity.

## Why NAND alone suffices

From De Morgan's laws ([[topics/boolean-algebra]]):
- NOT: `x̄ = (x*x)‾` (tie both NAND inputs together).
- AND: `x*y = ((x*y)‾)‾` (NAND, then NAND-as-NOT).
- OR: `x+y = (x̄*ȳ)‾` (NOT both inputs, then NAND).

Since {NOT, AND, OR} is already complete (any truth table can be written as
a canonical DNF using only these three), and all three are NAND-buildable,
NAND alone is complete. The same argument applies symmetrically to NOR.

## Practical use

The source works through minimizing the gate count for hardware built
entirely from NAND gates — relevant when manufacturing favors a single,
repeated gate type (e.g. standard-cell ASIC design) over mixed gate
libraries.

## Related pages

- [[topics/switching-functions-and-gates]]
- [[topics/boolean-algebra]]
