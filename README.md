# Acme Payments API

Acme Payments is a fictional company, and `openapi.yaml` is the OpenAPI 3 document of its made-up payments API: charges, refunds, customers and their cards, payouts and webhook endpoints. It exists to test [Since.dev](https://since.dev), which follows changes to APIs and finds the code they affect. It is not a real company or service. The host `api.acme-payments.example` uses the `.example` domain, which is reserved for documentation and never resolves, so nothing here can be called, and every change to the document is made on purpose to show a real kind of API change.

## Changelog

### 2.0.0

- `GET /v1/customers/{id}/cards` is removed. Use `GET /v1/customers/{id}/payment_methods`, which returns payment method objects (the card's details are under `card`). Adding a card with `POST /v1/customers/{id}/cards` is unchanged.
- `POST /v1/charges`: the `source` field is removed and `payment_method` is now required. A charge that named no card used to charge the customer's default card; it now fails, so pass the customer's `default_payment_method`.
- The charge object's `failure_message` is renamed to `failure_reason`. The payout object keeps `failure_message`.
- `GET /v1/charges` is deprecated and stops working on 2027-04-30. Use `GET /v1/charges/search`.
- `POST /v1/payouts` now requires an `Idempotency-Key` header.

### 1.0.0

- First version.
