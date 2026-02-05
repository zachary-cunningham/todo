Files in `ai_config` may never be changed without explicit approval. These are the highest level of settings for the AI. Level 0.

1. **Authority Hierarchy**
    - Level 1: `Core_Constraints/` (immutable, AI read-only)
    - Level 2: `02_System_Reality/` (must match code)
    - Level 3: `03_Intent_and_Roadmap/` (advisory)
    - Level 99: `99_AI_Artifacts/` (temporary, lowest authority)

If two documents conflict, the higher-authority document ALWAYS wins.

Lower-authority docs must be updated or discarded.

2. **Folder Semantics**
    - `docs/` = project understanding only
    - `ai_config/` = AI behaviour and rules

3. **Conflict Resolution Rules**
    - Higher level always wins
    - AI Artefacts may never instruct changes
    - AI may never create or modify files in Level 1
    - AI may only modify files in Levels 2–3 with explicit approval

4. **System Explained**
Documentation; how the project is set up; to be referenced before taking action.
- Core constraints; change slowly, define reality.
- System reality; starts blank with each new project, with example/sample explanations. Will be populated. To be referenced to understand the state of what exists.
    - With every update to the codebase, these files (in system reality) must be updated.
- Intent and Roadmap; guide decisions but don't override reality.

AI Config; how the AI must behave; may access these on each request to know how to process them.