Excellent! You've provided clear requirements. Let me gather the current state of your constraint files and create a plan to populate them properly. 

Read constraint templates

Read [](file:///Users/zacharycunningham/repos/todo/documentation/01_core_constraints/design_standards.md)

Read [](file:///Users/zacharycunningham/repos/todo/documentation/01_core_constraints/system_constraints.md)

Read [](file:///Users/zacharycunningham/repos/todo/documentation/01_core_constraints/technologies_and_frameworks.md)

Read [](file:///Users/zacharycunningham/repos/todo/documentation/01_core_constraints/backend_architecture/data_architecture.md)

Read [](file:///Users/zacharycunningham/repos/todo/documentation/01_core_constraints/backend_architecture/failure_and_security_model.md)

Read [](file:///Users/zacharycunningham/repos/todo/documentation/01_core_constraints/backend_architecture/request_response_flow.md)

Read [](file:///Users/zacharycunningham/repos/todo/documentation/01_core_constraints/backend_architecture/service_boundaries.md)

Read [](file:///Users/zacharycunningham/repos/todo/documentation/03_intent_and_roadmap/development_plan.md)

Read [](file:///Users/zacharycunningham/repos/todo/documentation/03_intent_and_roadmap/feature_specs.md)

Perfect! Now I can create a comprehensive plan to populate your core constraints based on your requirements.

---

## Plan: Populate Core Constraints for Local-First Todo App

You've provided clear technical and feature requirements. This plan structures those requirements into the appropriate constraint documents, establishing the immutable foundation before implementation begins. The local-storage architecture simplifies backend concerns significantly.

### Steps

1. **Define tech stack constraints** — Populate technologies_and_frameworks.md with TypeScript, React Native, Expo, React, and local storage approach (AsyncStorage/Expo SecureStore), explicitly documenting the no-backend decision and its implications

2. **Document Notion-inspired design system** — Fill design_standards.md with typography (clean sans-serif), spacing system (comfortable but not excessive), color palette (neutral with subtle accents), and gesture interactions (swipe left/right behaviors)

3. **Establish data architecture** — Create todo item schema in data_architecture.md defining fields (`id`, `title`, `completed`, `tags[]`, `dueDate`, `dueTime`, `profile`, `details`, `createdAt`, `completedAt`), local storage structure, and profile categories (work/home/habits)

4. **Define system constraints** — Populate system_constraints.md with data integrity rules (completed tasks stay in list, profile assignment required, gesture conflict prevention), and immutable behaviors (checkbox completion, swipe gestures, info icon visibility)

5. **Map feature specifications** — Create detailed specs in feature_specs.md for each interaction pattern (inline creation, swipe gestures, info popup, filtering, natural language parsing as Phase 2), with acceptance criteria and data flow

6. **Structure development phases** — Update development_plan.md with vision statement, MVP features (Phase 1: core CRUD + gestures + filtering), and Phase 2 (natural language recognition with date/time/tag extraction)

### Further Considerations

1. **Backend architecture files** — Since there's no backend/server, should we rename backend_architecture/ to `data_architecture/` or `local_storage_architecture/` to avoid confusion? Or document in each file that "N/A - local storage only"?

2. **Natural language parsing approach** — For Phase 2, do you have a preference for the NLP library (chrono-node, date-fns with parsing, compromise.js)? This might warrant a constraint if you want to avoid heavy dependencies.

3. **Profile switching UI** — How do users switch between work/home/habits views? Tab bar? Swipeable pages? This affects navigation architecture and should be in design standards.

4. **Filter persistence** — When users filter by due date or tags, should that filter persist when app reopens, or reset to "all tasks"? This is a data constraint decision.