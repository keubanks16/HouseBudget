# House Budget

Blank, fillable cost estimate worksheet / progress chart for our 40×60 barndominium (Barndominium Plan Set, Rev 0, Oct 27 2026): 2,400 sf main floor, 1,642 sf loft, 2,100 sf wraparound timber porches.

- Phases 1–4 with line items for this plan set (steel shell, wood framing, loft, stair, porches, windows/doors) with plan notes and quantities, plus inspection checkpoints
- Estimate, Actual Paid, auto Difference, Vendor, Date Complete and % done per item
- Phase subtotals, builder fee ($ or %), and running totals
- Edit mode to rename, add or remove items, sections, inspections and phases
- Build Steps tab: 82-step construction order in 9 stages for the steel shell + wood interior build with inspection gates, a "Next up" card and progress
- Cloud sync across devices via Firebase Firestore (project housebudget-a0972) using a private sync code
- Subs tab: line items grouped by trade with plan-based scope, sub contact info, and PDF export (all subs, or a per-sub scope sheet with bid lines; budget numbers optional)
- Saves automatically in the browser; Backup/Restore (JSON), CSV export and Print

Open `index.html` or the GitHub Pages site. On a phone, use Share → Add to Home Screen.

## Firestore rules (required for sync)

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /budgets/{code} {
      allow get: if code.size() >= 20;
      allow create, update: if code.size() >= 20
        && request.resource.data.json is string
        && request.resource.data.json.size() < 900000;
      allow list, delete: if false;
    }
  }
}
```
