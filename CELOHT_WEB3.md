# CeloHT / Web3 (matchids-celoht)

CeloHT is a dapp that lets people send and receive **CELO** and **USDm**
on the **Celo blockchain**. `matchids-celoht` makes CeloHT usable as a
Matchids payment method — for premium book purchases and Give Back
donations — by implementing the same `PaymentProvider` interface as
`matchids-payments`.

## What's real today

The provider structure, the interface contract, the "not configured"
fallback behavior, and the tests asserting that behavior. Nothing about
the actual CeloHT API call.

## What's intentionally NOT invented

Contract address, ABI, RPC endpoint, CeloHT API routes, wallet addresses,
private keys. `CeloHTProvider.isConfigured()` checks for
`CELOHT_API_BASE_URL` and `CELOHT_API_KEY`; until both are real,
`createIntent()` throws and `verifyTransaction()` always returns
`verified: false`.

## Activation checklist

See `matchids-celoht/docs/INTEGRATION.md` for the exact steps once
CeloHT's API details are available: fill in credentials, implement
`createIntent()` against CeloHT's real API, implement
`verifyTransaction()` against the Celo blockchain or CeloHT's
verification endpoint (server-side only), wire up `wallet.ts`'s
connection flow, then remove the "coming soon" label in `matchids-web`'s
checkout.

## Security specifics

- Wallet signing happens in the user's own wallet — this package never
  handles or stores a private key.
- Transaction verification never trusts a client-supplied "it worked."
