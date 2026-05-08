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

Duetto has a canonical set of abbreviations and display terms for hospitality metrics. These are used consistently across all products, documentation, and UI. When incorrect forms appear — in code strings, column headers, variable names, comments, or docs — fix them.

---

## Canonical Terminology Map

| Wrong (any of these) | Correct |
|---|---|
| RevPar, revpar, REVPAR, rev par, Rev Par | **RevPAR** |
| Pickup, Pick Up, Pick-up, Pick-Up, pickup, pick_up | **PU** |
| Average Lead Time, Avg Lead Time, Avg. Lead Time, avg_lead_time | **ALT** |
| Average Adults, Avg Adults, Avg. Adults, avg_adults | **AD** |
| Average Children, Avg Children, Avg. Children, avg_children | **CHD** |
| Total Guests, Total Guest, total_guests | **PAX** |
| Available Rooms, Avail Rooms, Avail. Rooms, avail_rooms | **AR** |

**RevPAR note:** The correct form is always `RevPAR` — never abbreviated further. It is not shortened to anything else. The most common mistake is wrong capitalisation (`RevPar`, `Revpar`).

---

## What to Fix

Apply corrections in:
- **UI display strings** — column headers, labels, tooltips, placeholder text
- **Code comments**
- **Object/variable names** where the metric name is the identifier (e.g. `avgLeadTime` → `alt`, `totalGuests` → `pax`, `pickupData` → `puData`)
- **AG Grid `headerName` fields**
- **HTML text content**
- **Documentation and markdown**

Use judgment for variable names — rename when the metric term is the primary meaning of the identifier. Don't rename if it would break external contracts (API response keys, localStorage keys, shared interfaces you don't own).

---

## Workflow

1. **Identify the scope.** If the user points at specific files, scan those. For the TravelCore RM Hub project, the relevant files are:
   - `travelcore-rm-hub.html`
   - `travelcore-rm-hub.css`
   - `travelcore-rm-hub.js`

2. **Grep for all wrong forms** before making any edits. Build a complete list of what needs to change.

3. **Apply corrections** file by file. For each file, make all replacements in a single pass.

4. **Report what changed.** After editing, produce a concise summary:
   - List each replacement made (wrong form → correct form, file, count)
   - Flag any cases where you held back (e.g. API key you didn't rename) and why

---

## Examples

**AG Grid column header:**
```js
// Before
{ field: 'revPar', headerName: 'RevPar' }
{ field: 'pickup', headerName: 'Pickup' }
{ field: 'avgLeadTime', headerName: 'Avg Lead Time' }

// After
{ field: 'revPar', headerName: 'RevPAR' }
{ field: 'pickup', headerName: 'PU' }
{ field: 'avgLeadTime', headerName: 'ALT' }
```

**HTML label:**
```html
<!-- Before -->
<span>Total Guests</span>
<th>Available Rooms</th>

<!-- After -->
<span>PAX</span>
<th>AR</th>
```

**Variable rename (when safe):**
```js
// Before
const avgAdults = row.averageAdults;
const totalGuests = summary.totalGuests;

// After
const ad = row.averageAdults;     // display-side variable renamed; source key unchanged
const pax = summary.totalGuests;  // same
```
