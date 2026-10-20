# Production architecture

## Recommended stack
- Mobile: React Native/Expo, TypeScript, secure device storage, certificate pinning
- API gateway: Kong or AWS API Gateway; OAuth 2.1/OIDC; device binding; rate limiting
- Services: NestJS/TypeScript for identity, ledger, payments, bills, savings, lending, market data, notifications
- Ledger: PostgreSQL double-entry ledger with immutable journal entries and idempotency keys
- Async: Kafka or AWS SQS/SNS; outbox pattern; dead-letter queue
- Cache: Redis without storing authoritative balances
- Secrets: AWS KMS + Secrets Manager; HSM-backed payment keys
- Observability: OpenTelemetry, SIEM, immutable audit logs and alerting

## Core boundaries
1. Identity/KYC: BVN/NIN through an authorised partner; tier and transaction limits; sanctions/PEP screening.
2. Wallet/ledger: every movement posts balanced debit/credit entries. Available balance is ledger-derived.
3. Transfers: licensed bank/MMO/PSSP partner, virtual accounts, name enquiry, webhook verification and reconciliation.
4. FX display: read-only NGN equivalents via an approved rate source; timestamp and disclose spread/source. Actual foreign-currency custody is a separate regulated product.
5. Bills/transport: provider adapters behind one orchestration interface. Each purchase has pending/success/failed/reversed states.
6. Savings: partner-led sub-wallet product; never imply deposit insurance unless contractually and legally valid.
7. Loans: licensed lender partner owns decisioning and disbursement. Show total cost, repayment schedule and complaints route before acceptance.
8. NGX: delayed or licensed market data, with timestamp and “information only” disclosure. Trading requires a licensed broker integration.

## Data model
User, Device, KycProfile, Wallet, LedgerAccount, Journal, JournalEntry, Beneficiary, Transfer, BillPayment, Provider, FxQuote, SavingsGoal, LoanOffer, Loan, Repayment, MarketInstrument, WatchlistItem, Consent, AuditEvent, WebhookEvent.

## Security acceptance gates
- No direct balance mutations; double-entry only
- MFA/biometrics plus transaction PIN and step-up checks
- Encryption in transit and at rest; tokenise sensitive data
- Idempotency on all money operations
- Signed webhooks with replay protection
- Velocity, beneficiary, device and behavioural fraud rules
- Daily automated reconciliation plus exception queue
- Least privilege, four-eyes production access and tamper-evident audit logs
- SAST, DAST, dependency and secret scans in CI; mobile and API penetration test before launch
- Tested backups, disaster recovery and incident response runbooks

## Delivery phases
- MVP: onboarding, NGN wallet, transfer, receive, FX view, airtime, electricity, transaction history
- Phase 2: savings, AI merchant payments, transport adapters, notifications, support/disputes
- Phase 3: lending marketplace, NGX watchlist, richer fraud scoring and business wallets
