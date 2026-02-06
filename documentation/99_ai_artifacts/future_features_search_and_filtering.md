# Future Features: Search and Filtering

**Status:** Deferred | Not in MVP scope

**Purpose:** Capture ideas for search and filter functionality to be implemented after core MVP is complete.

---

## Search/Filter Concepts

### Filter by Labels
- User can select one or multiple labels
- Display only todos that have matching labels
- UI: Label chips or dropdown selector

### Filter by Due Date
- User can filter by date ranges:
  - Today
  - This week
  - Overdue
  - Custom date range
- UI: Date range picker or preset buttons

### Search by Title/Details
- Text search across title and details fields
- Real-time filtering as user types
- Case-insensitive matching

---

## State Persistence

**Question for future:** Should active filters persist when app reopens?

**Options:**
- Persist in AsyncStorage under `@todo_app:app_state` key
- Reset to "show all" on app launch
- Remember per-session only

**Decision required before implementation.**

---

## UI Considerations

- Where to place filter controls? (Top bar, slide-out panel, modal)
- How to indicate active filters? (Badge count, visual highlight)
- Clear all filters button needed?

---

**Note:** This document is a placeholder for future planning. Do not implement until MVP is complete and approved.
