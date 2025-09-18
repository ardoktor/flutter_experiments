Here’s the lean spec for the first 2 screens.

1) Home (Pre-MVP)

Purpose: Show last maintenance at a glance and start new record fast.

Layout (top → bottom):

AppBar: title “Garage”, plate selector (optional later).

Card: Last Maintenance

date • km • total ₺

1–2 line summary (“oil + filter”, “front pads”)

Tap → Timeline

Row: Spend summary (numbers only)

“This month: ₺X” • “Last 3 mo: ₺Y”

Card: Notes (2 latest)

“Next: brake check @135k”

Tap → Record Details or Notes list (later)

FAB: “+ New Record”

Empty state: “No records yet” + big “Create first record” button.

Actions:

Tap Last Maintenance → Timeline

FAB → Create Record

Acceptance:

Loads in <300 ms with local data.

Shows last record correctly after restart.

FAB visible on all scroll positions.

2) Create Record (Add/Edit)

Purpose: Enter visit/problem, operations, costs; save in ≤30s.

Sections (field order):

Vehicle

Plate (text, required)

Visit

Date (today default, required)

Odometer KM (int, required)

Problem/Reason (short text, optional)

Operations & Costs

Items list (initially empty)

Button: Add item

Item sheet:

Type: part | labor (segmented)

Name (required)

Brand (optional)

Qty (default 1, numeric)

Unit price (TL, numeric)

Save → adds row name • qty × price = subtotal

Auto Total (sum of subtotals, read-only)

Notes (free text, optional)

Photos (max 3, optional; compress)

Bottom bar:

Left: Cancel

Right: Save

Validation:

Required: plate, date, km, at least one item with valid numbers.

No negative/NaN; km ≥ 0.

Total = exact sum of items.

On Save:

Persist to local store (Hive).

Navigate to Record Details (or back to Home with snackbar “Saved”).

Home updates Last Maintenance card.

Errors:

Inline field errors; toast for generic failures.

Unsaved changes → confirm dialog on back.

Performance:

Save <200 ms local.

PDF/share not in this screen (later).

Navigation flow

Home FAB → Create Record → Save → Record Details (then Back → Home).