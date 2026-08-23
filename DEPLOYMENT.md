# Deployment

Each repo deploys independently. This is a starting outline — see
`matchids-infrastructure` (phase 2) for the real CI/CD and infrastructure
setup once that repo exists.

| Repo | Suggested deployment |
|---|---|
| `matchids-web` | Any Next.js host (Vercel, etc.) — static/SSR hybrid |
| `matchids-admin` | Same as above, on a separate subdomain, ideally behind additional network restriction (VPN/IP allowlist) given its sensitivity |
| `matchids-backend` | Any Node host with outbound access to Postgres and the payment providers' APIs |
| `matchids-database` | Managed Postgres (RDS, Supabase, Neon, etc.) — migrations run from `matchids-backend`'s or `matchids-database`'s CI |
| `matchids-payments` / `matchids-celoht` | Published as private npm packages (or linked via workspace/submodule) — not deployed on their own |
| `matchids-content` | Not deployed — a data repo that CI validates and a sync process reads from |
| `matchids-design-system` | Published as a private npm package consumed by `matchids-web` / `matchids-admin` |

## Environment separation

Each deployable repo's `.env.example` lists exactly what it needs.
Staging and production should use entirely separate credentials for every
provider (database, card processor, CeloHT) — never share a production
key into a staging environment "temporarily."
