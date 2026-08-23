# Security Architecture

Cross-cutting security principles that apply across every Matchids repo.
Repo-specific detail lives in each repo's own README/SECURITY.md;
`matchids-security` (phase 2) will hold the full threat model and audit
documentation.

## Authentication & sessions

- Passwords hashed with bcrypt (cost factor 12) — see
  `matchids-backend/src/lib/auth.ts`.
- Sessions are JWTs signed with `AUTH_SECRET`, 7-day expiry.
- Admin routes require `requireAuth` **and** `requireAdmin` — a valid
  session alone isn't enough.

## Payment security

- **Never trust a client-reported payment success.** Every provider's
  `verifyTransaction()` is the sole path to confirming a payment, called
  only from `matchids-backend`'s webhook handler — see
  `architecture/PAYMENTS.md`.
- No processor or CeloHT credential is ever committed — see each repo's
  `.env.example`.
- Webhook signature verification (per-provider) is flagged as an
  explicit integration point in `matchids-backend`'s payment webhook
  controller, not silently skipped.

## Web3 security

- No private key is ever handled, stored, or logged by
  `matchids-celoht` — wallet signing happens client-side, in the user's
  own wallet.
- No contract address, ABI, or RPC endpoint is invented — see
  `architecture/CELOHT_WEB3.md`.

## API security

- `helmet` for standard HTTP security headers.
- Rate limiting on every route, tighter on `/api/auth/*`
  (`matchids-backend/src/middleware/rateLimit.ts`).
- All request bodies validated with Zod before touching business logic.
- The error handler never leaks a stack trace to the client in
  production.

## Data handling

- No production credentials, private user data, or secrets in any repo
  — see each repo's `.gitignore` and `.env.example`.
- Child-specific considerations are covered separately in
  `CHILD_SAFETY.md`.

## Reporting a vulnerability

See the `SECURITY.md` in each repo (or the organization's `.github`
repo, which provides the default for repos without their own).
