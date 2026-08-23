# Backend (matchids-backend)

Express + TypeScript API. One Express app (`src/app.ts`), routed by
resource (`src/routes/*.routes.ts`), with controllers holding the actual
logic (`src/controllers/*.controller.ts`).

## Layering

```
routes/       thin — just wiring a path to a controller + middleware
controllers/  request handling, calls into Prisma and PaymentService
middleware/   auth (JWT), admin gating, rate limiting, error handling
lib/          prisma client, auth helpers, PaymentService wiring, validation
```

## Auth

JWT bearer tokens issued at `/api/auth/login` and `/api/auth/register`.
`middleware/auth.ts` exposes `requireAuth` (any signed-in user) and
`requireAdmin` (role === "ADMIN", stacks on top of `requireAuth`).

## Payments

`src/lib/paymentService.ts` is the one place that registers
`@matchids/celoht`'s provider with `@matchids/payments`' `PaymentService`.
Controllers never talk to a payment provider directly — see
`architecture/PAYMENTS.md`.

## What's NOT here

- No frontend code — `matchids-web` and `matchids-admin` are separate
  apps that call this API.
- No canonical schema — that's `matchids-database`; this repo keeps a
  working copy (see its README for how to keep the two in sync).
