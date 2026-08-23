# API Reference — matchids-backend

Base URL: `NEXT_PUBLIC_API_URL` (default `http://localhost:4000`). All
bodies are JSON. Authenticated routes take `Authorization: Bearer <token>`.

## Auth

| Method | Path | Auth | Body |
|---|---|---|---|
| POST | `/api/auth/register` | — | `{ email, password, displayName }` |
| POST | `/api/auth/login` | — | `{ email, password }` |

Both return `{ token, user }`.

## Books & Categories

| Method | Path | Auth | Notes |
|---|---|---|---|
| GET | `/api/books` | — | Query: `category`, `access`, `language`, `q` |
| GET | `/api/books/:id` | — | 404 if not found |
| GET | `/api/categories` | — | |

## Kids Art

| Method | Path | Auth | Notes |
|---|---|---|---|
| GET | `/api/artwork` | — | Query: `category` |
| POST | `/api/artwork/:id/like` | required | Idempotent (upsert) |

## Orders & Payments

| Method | Path | Auth | Body |
|---|---|---|---|
| POST | `/api/orders` | required | `{ bookId, provider: "card" \| "celoht" }` — creates an order + payment intent, PENDING until verified |
| GET | `/api/orders` | required | Lists the caller's orders |
| POST | `/api/payments/webhook` | provider (signature check is an integration point) | `{ provider, providerReference }` — the only path that moves an order to PAID or a donation to CONFIRMED |

## Donations

| Method | Path | Auth | Body |
|---|---|---|---|
| POST | `/api/donations` | optional (guest donations allowed) | `{ amountCents, currency, campaignId?, provider }` |
| GET | `/api/donations/campaigns` | — | Active campaigns only |

## Library

| Method | Path | Auth |
|---|---|---|
| GET | `/api/library` | required — the caller's owned books |

## Notifications

| Method | Path | Auth | Notes |
|---|---|---|
| GET | `/api/notifications` | required | Placeholder — always returns `{ notifications: [] }` until a real model exists |

## Admin

| Method | Path | Auth | Notes |
|---|---|---|
| GET | `/api/admin/overview` | admin | Real counts from the database — see `matchids-admin`'s Overview page |

Additional admin endpoints (users, orders, payments, donations lists) are
integration points — see `architecture/ADMIN.md` for exactly what's
missing.
