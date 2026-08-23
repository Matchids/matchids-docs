# Architecture Overview

## The nine phase-1 repositories

```
matchids-web  ─────HTTP─────>  matchids-backend  ─────Prisma─────>  matchids-database
     │                              │
     │ imports tokens/components     ├── @matchids/payments  (card payments)
     ▼                              └── @matchids/celoht      (CELO / USDm on Celo)
matchids-design-system                    ▲
     ▲                                     │ implements PaymentProvider from
     │ imports tokens/components           │ @matchids/payments
matchids-admin  ─────HTTP─────>  matchids-backend (same instance)

matchids-content  ──(metadata + storage refs, no code coupling)──>  matchids-backend admin import path
matchids-docs  ── documents all of the above, no runtime dependency
```

## Repository responsibilities

| Repo | Responsibility | Depends on |
|---|---|---|
| `matchids-web` | Public site — frontend only | `matchids-backend` (HTTP), `matchids-design-system` |
| `matchids-backend` | API, auth, business logic, payment orchestration | `matchids-database` (schema), `matchids-payments`, `matchids-celoht` |
| `matchids-database` | Canonical schema, migrations, seed | none |
| `matchids-payments` | Provider-agnostic payment abstraction | none |
| `matchids-celoht` | Web3 (CeloHT) payment provider | implements `matchids-payments`' interface |
| `matchids-admin` | Internal dashboard | `matchids-backend` (HTTP), `matchids-design-system` |
| `matchids-content` | Book/artwork metadata + curation workflow | references `matchids-database`'s entity shapes |
| `matchids-design-system` | Tokens, Tailwind preset, components, brand assets | none |
| `matchids-docs` | Documentation for all of the above | none (documents, doesn't import) |

## Why polyrepo, not one monolith

Each repo has one clear owner-able responsibility, can be built, tested
and deployed independently, and — critically for a payments-adjacent
product — keeps sensitive logic (payment verification, database access)
out of anything that ships to a browser. See each repo's own README for
its internal structure.

## Cross-repo conventions

- **No secrets committed anywhere.** Every repo has a `.env.example`
  documenting exactly what it needs.
- **No invented data anywhere** — statistics, testimonials, partners,
  contract addresses, API endpoints. See `security/CHILD_SAFETY.md` and
  each repo's README for how unfinished features are represented
  honestly instead (a "coming soon" label, a documented integration
  point, an empty state).
- **Payment confirmation is always server-side**, always inside
  `matchids-backend`, always by calling into `matchids-payments`
  (which may delegate to `matchids-celoht`) — never trusted from a
  client request.
