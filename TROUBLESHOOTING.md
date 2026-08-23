# Troubleshooting

**`matchids-web` shows errors on checkout/donations pages.**
`matchids-backend` isn't running, or `NEXT_PUBLIC_API_URL` doesn't point
at it. This is expected behavior, not a bug — the frontend never fakes a
successful payment.

**Prisma client errors in `matchids-backend`.**
Run `npm run db:generate` after any schema change, and make sure
`prisma/schema.prisma` here matches the copy in `matchids-database` (see
that repo's README for sync strategies).

**"Unknown or unregistered payment provider" from PaymentService.**
`matchids-backend`'s `src/lib/paymentService.ts` didn't register a
provider — check that `@matchids/celoht` is actually linked and
imported.

**CeloHT checkout option always shows "coming soon."**
Expected until `CELOHT_API_BASE_URL` and `CELOHT_API_KEY` are set to real
values — see `matchids-celoht/docs/INTEGRATION.md`.

**Admin dashboard redirects to login immediately.**
The stored token is missing, expired, or belongs to a non-`ADMIN` user —
`matchids-backend` rejects the request and the token is cleared.

**`matchids-content`'s validate script fails in CI.**
A `metadata.json` doesn't match its schema — the error output names the
exact field. Check `schemas/book.schema.json` or
`schemas/artwork.schema.json`.
