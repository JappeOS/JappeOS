# Branching, Versioning & Release Policy

## Branches

| Branch | Purpose | Allowed Changes |
|---------|----------|----------------|
| `dev` | Active development (latest features, experiments) | Features, fixes |
| `testing` | Beta/testing stage for next stable update | Fixes only |
| `stable` | Production-ready branch | Critical fixes only |
| `feature/*` | Temporary feature branches merged into `dev` | New features |
| `fix/*` | Temporary fix branches merged into `dev` or directly into testing/stable if urgent | Bug/security fixes |

## Branch Flow

```
feature/* ─┐
fix/* ─────┼─→ dev ─→ testing ─→ stable
│
└───────→ tags/vX.Y.Z
```

- Only **fixes** can be applied to `testing` or `stable`.
- **Features** must go through `dev`.
- Merges flow **forward only** (`dev → testing → stable`).

## Versioning

- Semantic versioning: `vMAJOR.MINOR.PATCH`
- Example: `v1.4.2`
- Each release tagged on promotion (`tags/v1.4.2`)
- OS builds use the same branch as included packages:
  - `dev` OS build = all `dev` packages
  - `testing` OS build = all `testing` packages
  - `stable` OS build = all `stable` packages

## Releases

- Promotion path: `dev → testing → stable`
- Timing:
  - Automatic or manual promotion after stability period or QA approval
  - Example: every 2 weeks from `dev → testing`, monthly from `testing → stable`
- Tag each promoted version before merge.

## Rules

1. Always branch from `dev` unless doing a hotfix.
2. Only merge **forward** (no cherry-picking backward unless for a fix).
3. Tag before promotion to `testing` or `stable`.
4. Keep branches buildable and tested before merge.
