# Agent Rules

## Personality Config

## Errors and Unknowns Protocol

**Purpose:** Prevent confident guessing.

**AI must stop and ask if:**

- Requirements conflict or are ambiguous
- Multiple valid implementations exist with tradeoffs
- A decision would affect security, data integrity, or users
- Documentation is missing, stale, or contradictory

**AI may propose options when:**

- The decision is architectural or directional
- Tradeoffs are real and non-obvious
- No single choice is objectively correct

**AI must refuse to act when:**

- Requested action violates Core Constraints
- Required context is missing and cannot be inferred safely
- The task would require guessing about intent or system behavior

**Default behavior**

> When uncertain, do not assume. Ask or propose options. Never guess.
>

## File Management

## Writing Code

Must be in line with `01_core_constraints` .

Consult existing documentation in (`documentation/` folder), note how existing/similar code is written, follow that pattern.

Comment all code.

Must be modular.

Use existing code/functions as possible(even if needing to make slight adjustments to existing code to accommodate).

Must follow safety protocols.

Document the changes you make.

Maintain the `code_documentation.md` that explains every modular block of code, global and public variables (permissions) — allowed/disallowed actions. NOTE; as `code_documentation.md` is in `02_system_reality/`,  you may only make updates to the docs after explicit approval of your changes and potentially a few rounds of testing.

---

**Purpose:** Define what AI is allowed to change, and when it must stop.

**Change Classification**

- **Safe Changes (AI may act autonomously):**
    - Refactors with no behavior change
    - Naming, formatting, comments
    - Extracting reusable utilities
    - Performance improvements that preserve outputs
- **Restricted Changes (require explicit approval):**
    - Business logic changes
    - Data model or schema changes
    - Auth, permissions, security logic
    - API contracts or request/response shapes
    - UI/UX behavior changes
- **Forbidden Changes (AI must refuse):**
    - Modifying `01_Core_Constraints`
    - Removing security checks or validations
    - Changing invariants defined in System Reality
    - Silent behavior changes disguised as refactors

**Rule**

> If a change alters observable behavior, data meaning, or guarantees, AI must stop and request approval.
>

## Writing Docs

- All AI-generated documents (plans, reviews, summaries, analyses) must be created **only** in `99_AI_Artifacts`.
- Documents in `99_AI_Artifacts` are **lowest authority** and may **never** instruct or override changes.
- AI may **not** create or modify any document in `01_Core_Constraints`.
- If an authoritative document already exists:
    - **Do not create a new one.**
    - Propose updates **only** inside `99_AI_Artifacts`.
    - Modify documents in `02_System_Reality` or `03_Intent_and_Roadmap` **only with explicit approval**.
    - When modifying higher-level docs, clearly label changes as *AI-suggested and potentially incorrect*.
- If no authoritative document exists:
    - Create it **only** in `99_AI_Artifacts`.
    - It may be merged upward only after explicit approval.