# House Budget

Blank, fillable cost estimate worksheet / progress chart for a custom home build.

- Phases 1–4 with every line item from the original worksheet, plus inspection checkpoints
- Estimate, Actual Paid, auto Difference, Vendor, Date Complete and % done per item
- Phase subtotals, builder fee ($ or %), and running totals
- Edit mode to rename, add or remove items, sections, inspections and phases
- Build Steps tab: 75-step construction order in 7 stages with inspection gates, a "Next up" card and progress
- Cloud sync across devices via Firebase Firestore (project housebudget-a0972) using a private sync code
- Saves automatically in the browser; Backup/Restore (JSON), CSV export and Print

Open `index.html` or the GitHub Pages site. On a phone, use Share → Add to Home Screen.

## Firestore rules (required for sync)

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /budgets/{code} {
      allow get, create, update: if code.size() >= 20 && request.resource == null || code.size() >= 20 && request.resource.data.json is string && request.resource.data.json.size() < 900000;
      allow list, delete: if false;
    }
  }
}
```
