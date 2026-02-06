# Engineering Reference

## Core Invariants

**Protected Entities:** Users, Tasks, Evidence, Penalties, Reviewers, Transactions

## Forbidden Actions

### Task Creation
- ❌ Stake unavailable credits
- ❌ Create task with deadline < 15 minutes from now

### Task Editing
- ❌ Set deadline < 15 minutes from now
- ❌ Stake unavailable credits
- ❌ Edit within 30 minutes of deadline
- ⚠️ Must calculate stake delta (new - old) and adjust credits

### Task Deletion
- ❌ Delete within 30 minutes of deadline

### Evidence Submission
- ❌ Submit after deadline
- ❌ Submit empty/null evidence

### Credits
- ❌ Client-side penalty avoidance

## Authority Matrix

| Entity | Creator | Mutator | Immutable After |
|--------|---------|---------|-----------------|
| User | User | User | Never (soft delete only) |
| Task | User | User | 30m before deadline |
| Evidence | User | User | Deadline passes |
| Review | Reviewer | None | 15m after creation |
| Transaction | User/System | None | Creation |

## Mutation Rules

**User can:**
- Submit evidence (before deadline only)
- Edit/delete task (up to 30m before deadline)

**Reviewer can:**
- Approve or reject evidence (once only)

**System must:**
- Trigger penalty immediately at deadline if no evidence

## Server-Side Only

- All credit operations (stake, return, burn)
- Authentication (registration, sign-in)
- Task CRUD operations
- Evidence approval/rejection

## Time-Based Events

- Penalty trigger at deadline (no evidence present)

## Append-Only Data

- Evidence submissions
- Transactions (stake, burn, return)
- Review decisions

## Failure Tolerance

**May fail:** UI, Notifications

**Must never fail:** Deadline enforcement, Evidence integrity, Penalty accuracy, Credit transfers

## Scalability Deferred

- Moderation volume
- Evidence storage

## Must Remain Configurable

- Business rules
- Penalty severity
- Review assignment logic

## Schema (Minimal Fields)

```
User
  id, username, email, verified, created_at, credits

Task
  id, user_id, title, description, stakes, due_at, 
  status: [pending | awaiting_review | completed | failed],
  created_at

Evidence
  id, task_id, media_url, submitted_at

Reviewer
  id, evidence_id, reviewer_id, 
  decision: [approved | rejected],
  decided_at

Transaction
  id, user_id, task_id (nullable), amount,
  kind: [stake | return | burn | topup],
  created_at
```

## Task Lifecycle

1. Create → stake credits immediately
2. Deadline passes without evidence → penalty triggered by system
3. Evidence submitted → status = awaiting_review
4. Review approved → credits returned, status = completed
5. Review rejected → credits burned, status = failed

## Credit Flow Rules

- **Stake:** Deduct from user.credits immediately on task creation
- **Return:** Add to user.credits on evidence approval
- **Burn:** Credits already deducted; no user.credits change on failure
- **Stake Edit:** Calculate delta, adjust user.credits accordingly
- **Delete:** Return full stake to user.credits

## Account Management

- New accounts: unverified by default
- Unverified accounts: wiped every 24 hours
- Sign-in: email OTP only
