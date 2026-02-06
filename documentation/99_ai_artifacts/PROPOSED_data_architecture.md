# Data Architecture

**Status:** AI-proposed | Awaiting approval for merge to `01_core_constraints/backend_architecture/`

**Purpose:** Define immutable data models and local storage structure. All data operations must conform to this schema.

---

## Todo Item Schema

```typescript
interface TodoItem {
  id: string;                    // UUID v4
  title: string;                 // Max 500 characters
  completed: boolean;            // Default: false
  labels: string[];              // Max 5 labels per item
  dueDate: string | null;        // ISO 8601 date: YYYY-MM-DD
  dueTime: string | null;        // ISO 8601 time: HH:mm
  details: string;               // Max 200 characters
}
```

---

## Local Storage Structure

### Storage Keys

```
@todo_app:items          // Array of TodoItem objects
@todo_app:app_state      // App configuration and UI state
```

### Data Format

**`@todo_app:items`**
```json
[
  {
    "id": "uuid

```
@todo_app:items          // Array of TodoItem objects
```

### Data Format

```json
[
  {
    "id": "uuid-v4-string",
    "title": "Water plants",
    "completed": false,
    "labels": ["daily", "garden"],
    "dueDate": "2026-02-05",
    "dueTime": "14:30",
    "details": "Remember to water the ferns in the living room"
  }
]
### Optional Fields
- `tags` — Empty array if no tags
- `dueDate` — null if no date set
- `dueTime` — null if no time set (requires dueDate if present)
- `details` — Empty string if no details
- `completedAt` — null until completed=true, then set to timestamp

### Validation Rules
1. If `dueTime` is set, `dueDate` must also be set
2. `completedAt` must be null if `completed=false`
3. `completedAt` must be non-null if `completed=true`
4. `tags` array cannot contain duplicates
5. `tags` cannot contain empty strings
6. Profile dropdown at top controls which items display (filter by profile)

---

## Storage Operations

### Write Operations
- **Create:** Generate UUID, set `createdAt`, default `completed=false`
- **Update:** Modify mutable fields only (title, tags, dueDate, dueTime, details, profile)
- **Complete:** Set `completed=true`, set `completedAt=now()`
- **Uncomplete:** Set `completed=false`, set `completedAt=null`
- **Delete:** Remove item from array, write updated array
, max 500 characters
- `completed` — Boolean only

### Optional Fields
- `labels` — Empty array if no labels, max 5 labels per item
- `dueDate` — null if no date set
- `dueTime` — null if no time set (requires dueDate if present)
- `details` — Empty string if no details, max 200 characters

### Validation Rules
1. If `dueTime` is set, `dueDate` must also be set
2. `labels` array cannot exceed 5 items
3. `labels` array cannot contdefault `completed=false`
- **Update:** Modify mutable fields (title, labels, dueDate, dueTime, details)
- **Complete:** Set `completed=true`
- **Uncomplete:** Set `completed=false`
- **Delete:** Remove item from array, write updated array

### Read Operations
- **Load all:** Read `@todo_app:items`, parse JSON, validate schema
- **Display:** Completed items pushed to bottom of list

### Data Integrity
- Every write operation must:
  1. Validate schema before writing
  2. Handle AsyncStorage errors gracefully
  3. Maintain atomic updates (read → modify → write)
  4. Never partially update (write full array or nothing)

### Initialization
- If `@todo_app:items` not found, initialize as empty array `[]`
2. **IDs are permanent** — Never reuse deleted IDs
3. **Arrays are non-nullable** — Empty array [], never null
4. **Label limit enforced** — Maximum 5 labels per todo item
5. **Character limits enforced** — title max 500, details max 200