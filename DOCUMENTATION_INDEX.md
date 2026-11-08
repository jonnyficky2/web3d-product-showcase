# Forma Documentation Index

This index is the entry point for the project documentation system.

## Primary sources of truth

| Topic | Authoritative document |
|---|---|
| Current implementation state | [Project State](docs/project/PROJECT_STATE.md) |
| Product intent and requirements | [Product Requirements](docs/product/PRD.md) |
| Active work | [Task Board](docs/project/TASK_BOARD.md) |
| Runtime architecture | [System Architecture](docs/architecture/SYSTEM_ARCHITECTURE.md) |
| Security posture | [Security Audit](docs/security/SECURITY_AUDIT.md) |
| Verification status | [QA Report](docs/testing/QA_REPORT.md) |
| AI agent rules | [AI Instructions](docs/ai/AI_INSTRUCTIONS.md) |

## Documentation map

- Product: [PRD](docs/product/PRD.md), [Requirements](docs/product/REQUIREMENTS.md), [User Stories](docs/product/USER_STORIES.md), [Acceptance Criteria](docs/product/ACCEPTANCE_CRITERIA.md), [Feature Specifications](docs/product/FEATURE_SPECIFICATIONS.md)
- Project: [Overview](docs/project/PROJECT_OVERVIEW.md), [State](docs/project/PROJECT_STATE.md), [Task Board](docs/project/TASK_BOARD.md), [Task Template](docs/project/TASK_TEMPLATE.md), [Execution Protocol](docs/project/TASK_EXECUTION_PROTOCOL.md), [Dependencies](docs/project/TASK_DEPENDENCIES.md), [Sprint Plan](docs/project/SPRINT_PLAN.md), [Progress](docs/project/PROGRESS_REPORT.md), [Blockers](docs/project/BLOCKERS.md), [Roadmap](docs/project/ROADMAP.md), [Workflow](docs/project/DEVELOPMENT_WORKFLOW.md), [DoD](docs/project/DEFINITION_OF_DONE.md), [Session Log](docs/project/SESSION_LOG.md), [Milestones](docs/project/MILESTONES.md)
- Architecture: [System Architecture](docs/architecture/SYSTEM_ARCHITECTURE.md), [Tech Stack](docs/architecture/TECH_STACK.md), [Data Flow](docs/architecture/DATA_FLOW.md), [API Documentation](docs/architecture/API_DOCUMENTATION.md), [Database Schema](docs/architecture/DATABASE_SCHEMA.md), [ADRs](docs/architecture/adr/)
- Design: [Design System](docs/design/DESIGN_SYSTEM.md), [UI Specifications](docs/design/UI_SPECIFICATIONS.md), [UX Flows](docs/design/UX_FLOWS.md), [Component Catalog](docs/design/COMPONENT_CATALOG.md)
- Engineering: [Coding Standards](docs/engineering/CODING_STANDARDS.md), [Development Guidelines](docs/engineering/DEVELOPMENT_GUIDELINES.md), [Error Handling](docs/engineering/ERROR_HANDLING.md), [Technical Debt](docs/engineering/TECHNICAL_DEBT.md)
- Testing: [Strategy](docs/testing/TEST_STRATEGY.md), [Plan](docs/testing/TEST_PLAN.md), [Cases](docs/testing/TEST_CASES.md), [QA Report](docs/testing/QA_REPORT.md)
- Security: [Requirements](docs/security/SECURITY_REQUIREMENTS.md), [Threat Model](docs/security/THREAT_MODEL.md), [Audit](docs/security/SECURITY_AUDIT.md)
- Audits: [Repository Audit](docs/audit/REPOSITORY_AUDIT.md), [UI Audit](docs/audit/UI_AUDIT.md), [Performance Audit](docs/audit/PERFORMANCE_AUDIT.md), [Action Plan](docs/audit/AUDIT_ACTION_PLAN.md)
- AI: [Instructions](docs/ai/AI_INSTRUCTIONS.md), [Project Context](docs/ai/PROJECT_CONTEXT.md), [Workflow](docs/ai/AI_WORKFLOW.md)
- Operations: [Build/Deployment](docs/operations/BUILD_DEPLOYMENT.md), [Release Checklist](docs/operations/RELEASE_CHECKLIST.md), [Operations Changelog](docs/operations/CHANGELOG.md), [Incident Log](docs/operations/INCIDENT_LOG.md)

## Taxonomy mapping

The repository already had a domain-oriented `docs/` structure before the numbered taxonomy was requested. To avoid duplicate sources of truth, the existing domain folders are canonical: `docs/project/` is planning, `docs/architecture/` is architecture, `docs/audit/` is audits, and so on. Compatibility documents such as `API_SPECIFICATION.md` and `USER_FLOWS.md` point to the canonical documents.

The root [AGENTS.md](AGENTS.md) is the primary agent instruction file.

## Legacy documents preserved

- [README](README.md)
- [Legacy Architecture](docs/ARCHITECTURE.md)
- [Legacy PRD](docs/PRD.md)
- [Legacy User Flow](docs/USER_FLOW.md)
- [Legacy Taskboard](docs/TASKBOARD.md)

These remain historical/useful references. New work should update the primary documents above first.
