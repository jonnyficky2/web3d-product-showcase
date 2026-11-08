# Task Execution Protocol

When the user names a task or milestone, follow this protocol.

1. **Identify:** Resolve the exact permanent ID in `TASK_BOARD.md`.
2. **Read context:** Read `PROJECT_STATE.md`, requirements, architecture, and the task detail file.
3. **Verify:** Inspect source and confirm every dependency is actually complete.
4. **Plan:** Define the smallest implementation and verification steps.
5. **Execute:** Change only the task scope; never silently expand it.
6. **Test:** Run available tests, lint, type checks, builds, or explicit manual checks.
7. **Verify acceptance:** Check every criterion one by one.
8. **Document:** Update affected requirements, architecture, QA, and audit docs.
9. **Update status:** Synchronize task detail, board, milestone, project state, session log, and changelog as appropriate.
10. **Report:** List modified files, evidence, test results, remaining risks, and next eligible tasks.

## Command interpretation

- `Execute TASK-012`: execute only that task.
- `Continue TASK-012`: resume recorded progress; do not restart completed steps.
- `Execute MILESTONE-003`: execute eligible tasks in dependency order.
- `Execute all P0`: execute eligible P0 tasks without bypassing dependencies.
- `Audit TASK-012`: verify implementation and acceptance criteria without changing source unless separately authorized.
- `Update taskboard`: reconcile docs against source evidence.
- `Execute next task`: choose highest-priority eligible task, then earliest milestone order.

Unknown or ambiguous IDs require clarification. Never mark `DONE` without evidence.
