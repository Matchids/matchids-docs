# Database (matchids-database)

Postgres via Prisma. See that repo's `README.md` and `docs/ERD.md` for
the full entity list and relationships — this page is the short version
for orientation.

## Core entities

`User`, `Category`, `Book`, `UserLibrary`, `Artwork`, `ArtworkLike`,
`Order`, `OrderItem`, `Payment`, `PaymentTransaction`, `DonationCampaign`,
`Donation`, `VerifiedOrganization`, `ImpactReport`.

## Modeling rules

- Money as integer cents, never floats.
- Enums for closed sets, not free-text strings.
- `isDemoContent` on any seedable content table.
- `VerifiedOrganization` and `ImpactReport` start empty and stay empty
  until there's something real to put in them — the frontend must never
  render placeholder rows from these tables.

## Keeping matchids-backend in sync

`matchids-backend` keeps a working copy of `schema.prisma`. The team
should pick one sync strategy (git submodule, published package, or a CI
job) and document it — see `matchids-backend`'s README for the options.
