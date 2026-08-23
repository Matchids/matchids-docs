# Content Management (matchids-content)

Where the content team works: book and artwork metadata, validated
against JSON schemas, kept separate from both the database (which holds
what's live in production) and from any large binary files (PDFs,
images — see `matchids-content/docs/STORAGE.md`).

## Workflow

1. Add or edit a `metadata.json` under `books/<id>/` or `artwork/<id>/`.
2. CI validates it against `schemas/book.schema.json` or
   `schemas/artwork.schema.json` on every PR.
3. Set `status` to `draft` → `in_review` → `published` as it moves
   through review.
4. Upload the actual PDF/image to object storage / `matchids-images`,
   referencing it by key — never commit the binary here.
5. A sync step (not yet built — see `docs/STORAGE.md`) imports
   `published` entries with a real storage reference into
   `matchids-database` via `matchids-backend`'s admin API.

## No invented content

Every real entry needs Matchids to actually have rights to publish it.
The `_sample-` entries in each folder are worked examples, not real
content, and are named so they can't be mistaken for it.
