# Contributing Across Matchids Repos

Each repo has its own `CONTRIBUTING.md` with setup specifics. These rules
apply everywhere:

1. **Never commit secrets.** Every repo's `.env.example` documents what
   it needs — real values only ever go in a local `.env` or a deployment
   platform's secret store.
2. **Never invent data.** No fake statistics, testimonials, partner
   organizations, contract addresses, or API endpoints. Mark unfinished
   integrations explicitly (see `matchids-celoht/docs/INTEGRATION.md`
   for the pattern).
3. **Payment confirmation stays server-side**, always. If you're touching
   `matchids-backend`, `matchids-payments`, or `matchids-celoht`, re-read
   `security/SECURITY.md` before changing anything on that path.
4. **Content involving children gets reviewed for age-appropriateness**
   before merging — this applies to `matchids-content` and any UI copy
   in `matchids-web`.
5. **Keep the repo split intentional.** If a change feels like it belongs
   in a different repo (e.g. payment logic creeping into
   `matchids-web`), that's worth raising before merging, not after.
