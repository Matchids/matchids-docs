# Admin (matchids-admin)

Separate Next.js app for platform administration: Books, Categories,
Kids Art, Users, Orders, Payments, Donations, Donation Campaigns,
Featured Content, Platform Settings.

## Why separate from matchids-web

Different audience, different security posture (every route requires an
authenticated `ADMIN`-role account, enforced by `matchids-backend`), and
no reason to ship admin code in the public site's bundle.

## Current state

Overview, Books, Categories, Kids Art and Donation Campaigns read real
data from `matchids-backend`. Users, Orders, Payments and Donations are
placeholders — matchids-backend doesn't have admin list endpoints for
those yet; each placeholder page names the exact endpoint to add.
Featured Content and Platform Settings are placeholders pending a data
model.

## Auth

Same JWT login as `matchids-web`'s eventual account system, posted to
`matchids-backend`'s `/api/auth/login`. The backend enforces the
`ADMIN` role check; the admin app just refuses to render without a valid
token. See `matchids-admin/README.md` for the production-hardening note
about moving the token out of `localStorage`.
