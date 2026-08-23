# Getting Started — Running the Full Stack Locally

Clone the repos you need (at minimum: `matchids-database`,
`matchids-payments`, `matchids-celoht`, `matchids-backend`,
`matchids-web`). All commands assume Node 18+.

## 1. Database

```bash
cd matchids-database
npm install && npm run generate
cp .env.example .env   # point DATABASE_URL at a local Postgres
npm run push
npm run seed            # demo content only
```

## 2. Payment packages

```bash
cd matchids-payments && npm install && npm test
cd ../matchids-celoht && npm install && npm test
```

Link both into `matchids-backend` — with npm workspaces, or
`npm link` / a `file:../matchids-payments` dependency for standalone
polyrepo development.

## 3. Backend

```bash
cd matchids-backend
npm install
cp .env.example .env
cp ../matchids-database/prisma/schema.prisma prisma/schema.prisma
npm run db:generate
npm run dev              # http://localhost:4000
```

## 4. Frontend(s)

```bash
cd matchids-web
npm install
cp .env.example .env      # NEXT_PUBLIC_API_URL=http://localhost:4000
npm run dev                # http://localhost:3000

cd ../matchids-admin
npm install
cp .env.example .env
npm run dev                 # http://localhost:3001
```

## Creating an admin account

There's no public admin sign-up flow, intentionally. Register a normal
account via `matchids-web` or `POST /api/auth/register`, then promote it
to `ADMIN` directly via Prisma Studio (`npx prisma studio` in
`matchids-backend`) during development.

## Common gotchas

See `TROUBLESHOOTING.md`.
