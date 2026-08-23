# Child Safety & Privacy

Because Matchids serves children, this isn't a bolt-on policy — it
shapes the architecture itself.

## Content review

Every book and artwork entry in `matchids-content` carries a `status`
(`draft` → `in_review` → `published`); only published, reviewed content
is meant to reach `matchids-database` and, from there, real users. See
`architecture/CONTENT_MANAGEMENT.md`.

## Parental controls

`matchids-database`'s `User` model supports a parent → child relationship
(`parentId` / `children`), so a parent account can hold and manage child
profiles rather than children creating fully independent accounts.

## Minimal data collection

Matchids collects what's needed to run the product — account details,
purchase history, donation records — and nothing more. No behavioral
tracking or third-party advertising targeted at child accounts.

## Safe interactions

The current architecture (phase 1) has no open social features between
users — no public profiles, comments, or messaging. If social features
are added later, they need their own safety review before being built,
not after.

## Honesty in what's shown to families

No fake testimonials, statistics, partner organizations, or donation
results anywhere in the product — a parent evaluating whether to trust
Matchids with their child's data and their donation deserves accurate
information, not marketing embellishment. See each repo's README for how
this is enforced (e.g. `VerifiedOrganization` and `ImpactReport` staying
empty until real).

## Reporting a concern

The `matchids-web` Contact page is the current path for a parent or
guardian to report content or behavior that seems unsafe. A dedicated
moderation/report queue is a natural phase 2 addition once volume
justifies it.
