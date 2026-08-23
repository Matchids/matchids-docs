# Payments (matchids-payments)

The provider-agnostic abstraction every payment method in Matchids
implements — card payments and CeloHT alike.

## The interface

```ts
interface PaymentProvider {
  readonly id: PaymentProviderId;
  isConfigured(): boolean;
  createIntent(request: PaymentIntentRequest): Promise<PaymentIntentResult>;
  verifyTransaction(providerReference: string): Promise<PaymentVerificationOutcome>;
  refund?(providerReference: string, amountCents: number): Promise<RefundResult>;
}
```

`matchids-backend` holds one `PaymentService` instance, registers every
provider (`CardProvider` from this repo, `CeloHTProvider` from
`matchids-celoht`) against it, and never imports a provider directly.

## Non-negotiable rules

1. **`isConfigured()` must be honest.** A provider without real
   credentials returns `false`, and callers are expected to hide that
   payment method rather than offer something that can't work.
2. **`verifyTransaction()` is the only path to a confirmed payment.**
   It always re-checks with the provider (webhook signature + status for
   cards, on-chain or provider-side lookup for CeloHT) and is only ever
   called from trusted backend code — never trust a client's report that
   a payment succeeded.
3. **Refunds are opt-in** (`refund?` is optional on the interface) so a
   provider that doesn't support them yet can say so explicitly instead
   of silently failing.

See `architecture/CELOHT_WEB3.md` for the Web3-specific details.
