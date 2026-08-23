# Project Vision

**A Digital World Where Children Learn, Imagine, Create and Give**

Matchids is an international digital platform for children, parents and
communities, founded by **Suzie Matchilda George**. It brings together
four things that don't usually live in one product:

- **Learn** — a digital library of free and premium books, organized by
  age, language and category.
- **Imagine** — Kids Art: coloring pages, creative prompts and activities.
- **Create** — a platform built to grow with real content and real
  features, not placeholders dressed up to look finished.
- **Give** — the Give Back program, directing part of what Matchids earns
  toward children in orphanages who need it most.

## What makes this hard to get right

Matchids sits at the intersection of a few things that each demand their
own discipline: content for children (age-appropriateness, trust),
payments (traditional cards *and* Web3 through CeloHT — CELO and USDm on
the Celo blockchain), and social impact (donations that have to be real
and traceable, never dressed up with invented numbers).

The repo split reflects that: `matchids-payments` and `matchids-celoht`
are separate from each other and from `matchids-backend` precisely so
neither payment method can accidentally cut corners the other doesn't.
`matchids-content` keeps book/artwork curation separate from the code
that serves it, so the content team's workflow doesn't require touching
the database directly.

## What "done" looks like for phase 1

Every phase 1 repo (`matchids-web`, `-backend`, `-database`, `-payments`,
`-celoht`, `-admin`, `-content`, `-design-system`, `-docs`) builds,
tests, and documents an honest slice of the product — real pages, a real
API, a real schema, real provider interfaces — with every unfinished
integration point named explicitly rather than faked. Phase 2
(`matchids-infrastructure`, `-security`, `-mobile`) builds on that
foundation once it's solid, not before.
