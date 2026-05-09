---
name: duetto-terminology
description: >
  Enforces correct Duetto hospitality terminology in code, UI labels, column
  headers, comments, and documentation. Use this skill whenever working with
  Duetto metrics or KPIs — in code strings, variable names, AG Grid column
  definitions, HTML display text, or any written content. Trigger on requests
  like "fix terminology", "correct the labels", "apply Duetto terms", or any
  time you see or write RevPar, Pickup, Average Adults, Average Children,
  Total Guests, Available Rooms, or Average Lead Time in any form. Also apply
  proactively when generating new column definitions or metric labels for
  Duetto products.
---

# Duetto Terminology Enforcer

Duetto has canonical terms for hospitality metrics. Two rules govern how they appear:

1. **RevPAR** — always written as `RevPAR`, in every context, with no exceptions. Never abbreviated further, never written as RevPar, Revpar, REVPAR, etc.
2. **All other metrics** — use the full term when space allows; fall back to the abbreviation only in space-constrained contexts (tight column headers, compact labels, small UI cells).

---

## Canonical Terms

| Full term (default) | Abbreviation (space-constrained only) | Wrong forms to fix |
|---|---|---|
| **RevPAR** | *(none — always RevPAR)* | RevPar, revpar, REVPAR, rev par, Rev Par |
| **Pickup** | **PU** | Pick Up, Pick-up, Pick-Up, pick_up |
| **Average Lead Time** | **ALT** | Avg Lead Time, Avg. Lead Time, avg_lead_time |
| **Average Adults** | **AD** | Avg Adults, Avg. Adults, avg_adults |
| **Average Children** | **CHD** | Avg Children, Avg. Children, avg_children |
| **Total Guests** | **PAX** | Total Guest, total_guests |
| **Available Rooms** | **AR** | Avail Rooms, Avail. Rooms, avail_rooms |

---

## When to use full vs. abbreviated form

**Use the full term** (default) for:
- Tooltip text, modal labels, sidebar labels, form field labels
- Documentation, comments, markdown
- Any label or heading with generous width

**Use the abbreviation** only when:
- The column or cell is explicitly narrow/fixed-width (e.g. a compact AG Grid column)
- The UI container makes the full term visually cramped or truncated
- The surrounding columns already establish an abbreviation-only convention

**RevPAR never follows this rule** — it is always `RevPAR` regardless of context.

---

## What to Fix

Apply corrections in:
- **UI display strings** — column headers, labels, tooltips, placeholder text
- **Code comments**
- **AG Grid `headerName` fields**
- **HTML text content**
- **Documentation and markdown**
- **Variable/object names** where the metric term is the primary identifier — rename when safe (don't rename API response keys, localStorage keys, or shared interfaces you don't own)

---

## Workflow

1. **Identify the scope.** Scan the files the user points at, or the current working directory if none are specified.

2. **Grep for all wrong forms** before making any edits.

3. **Apply corrections** file by file, choosing full vs. abbreviated form based on context.

4. **Report what changed** — list each replacement (wrong form → correct form, file, count) and flag any cases where you held back and why.

---

## Broader Industry Reference

For wider hospitality industry terminology beyond the Duetto-specific map above — including distribution, sales, inventory, pricing, and forecasting terms — see [`references/industry-terminology.md`](references/industry-terminology.md).

Duetto's canonical map always takes precedence where the two conflict.

---

## Examples

**AG Grid — narrow column uses abbreviation; RevPAR always stays RevPAR:**
```js
// Before
{ field: 'revPar',      headerName: 'RevPar' }
{ field: 'pickup',      headerName: 'Pickup' }
{ field: 'avgLeadTime', headerName: 'Avg Lead Time' }

// After (narrow/compact grid)
{ field: 'revPar',      headerName: 'RevPAR' }       // always RevPAR
{ field: 'pickup',      headerName: 'PU' }            // abbreviated — narrow column
{ field: 'avgLeadTime', headerName: 'ALT' }           // abbreviated — narrow column

// After (wide/spacious grid)
{ field: 'revPar',      headerName: 'RevPAR' }        // still always RevPAR
{ field: 'pickup',      headerName: 'Pickup' }        // full term — space available
{ field: 'avgLeadTime', headerName: 'Average Lead Time' }
```

**Tooltip / label (always full term):**
```html
<!-- Before -->
<span title="Total Guests">PAX</span>
<label>Avg Adults</label>

<!-- After -->
<span title="Total Guests">Total Guests</span>
<label>Average Adults</label>
```
