# Task Dependencies

## Dependency graph

```mermaid
flowchart TD
  T101[TASK-101 Scene] --> T102[TASK-102 Products]
  T101 --> T105[TASK-105 Controls]
  T102 --> T103[TASK-103 Switching]
  T102 --> T104[TASK-104 Color]
  T101 --> T001[TASK-001 Fallback]
  T101 --> T006[TASK-006 Baseline]
  T105 --> T006
  T006 --> T002[TASK-002 Performance budget]
  T002 --> T007[TASK-007 Adaptive tuning]
  T001 --> T003[TASK-003 Smoke tests]
  T103 --> T201[TASK-201 Camera tween]
  T201 --> T202[TASK-202 Snapshot]
  T101 --> T203[TASK-203 Disposal]
  T105 --> T204[TASK-204 Reduced motion]
```

## Critical sequence

`TASK-101 -> TASK-102 -> TASK-103 -> TASK-201 -> TASK-202`

## Independent eligible tasks

`TASK-001`, `TASK-004`, and `TASK-205` can begin without an unfinished blocking dependency. `TASK-006` is eligible because TASK-101 and TASK-105 are DONE.

## Circular dependency check

No circular dependencies found in the current graph.
