# Subscription Commerce Platform

> Part of the [worlds-biggest-software-project](https://github.com/worlds-biggest-software-project) initiative.
>
> An AI-native, open-source platform for managing recurring commerce — subscriptions, churn prevention, dunning, and pause/resume flows.

Subscription Commerce Platform is a candidate open-source project for businesses running recurring-revenue models, from DTC subscription boxes to SaaS billing teams. It targets the gap between developer-friendly billing APIs and the intelligent, retention-focused tooling that enterprise incumbents charge a premium for.

---

## Why Subscription Commerce Platform?

- Incumbent platforms split along narrow lines: Recharge is Shopify-only, Stripe Billing is light on churn prevention, Zuora is enterprise-priced and slow to implement, and Churnkey solves only the cancellation flow.
- Pricing is steep and opaque: mid-tier platforms run $250–$600/month, enterprise contracts reach $10K–$100K+/year, and transaction-percentage models (Recharge, Paddle) scale costs linearly with GMV.
- Intelligent dunning, churn prediction, and personalised retention offers are mostly locked behind proprietary ML in tools like Recurly's Revenue Optimization Engine.
- Subscription customers deliver roughly five times the lifetime value of one-time buyers, yet most teams still rely on static retry schedules and generic cancellation flows.
- An open, standards-aligned alternative (PCI DSS, SCA/PSD2, ASC 606, GDPR) would let merchants combine a developer-first API with AI-driven retention without vendor lock-in.

---

## Key Features

### Subscription Lifecycle & Billing

- Subscription create, update, renew, and cancel flows
- Flexible billing intervals (monthly, annual, custom) and usage-based / metered models
- Trial periods and promotional pricing support
- Recurring and one-time charges with coupon and discount management
- Multi-currency billing for international merchants

### Payments, Dunning & Retry

- Payment gateway integration (Stripe, PayPal, and others) with abstraction across providers
- Payment retry automation with configurable schedules
- ML-powered intelligent dunning that optimises retry timing and messaging
- Churn prediction scoring per subscriber

### Subscriber Self-Service

- Customer portal for payment updates, history, and plan changes
- Pause, skip, and frequency-adjustment controls to reduce involuntary cancellations
- One-click checkout experience
- Personalised pause and downgrade offers at cancellation intent

### Revenue Operations & Compliance

- Invoice generation, delivery, and receipt management
- Revenue recognition support aligned with ASC 606 / IFRS 15
- International tax and VAT handling
- Cohort analysis, LTV, retention curves, and revenue analytics

### Integration & Extensibility

- REST API for custom subscription workflows
- Webhook events for event-driven integrations
- Connectors for e-commerce platforms and accounting systems
- Admin dashboard for operations teams

---

## AI-Native Advantage

The platform treats AI as a core capability rather than an add-on. It predicts involuntary churn risk per subscriber before payment failure occurs, dynamically optimises dunning retry timing and messaging based on behavioural and card-type signals, and generates personalised pause or downgrade offers calibrated to each subscriber's price sensitivity. LLM-assisted contract analysis automates revenue recognition entries for mid-cycle amendments, while anomaly detection flags duplicate charges and fraudulent subscriptions in real time.

---

## Tech Stack & Deployment

The project targets a self-hostable, API-first architecture that integrates with existing payment gateways rather than acting as a payment processor. Expected alignment with PCI DSS for stored payment methods, SCA/PSD2 for EU recurring authentication, ISO 20022 for bank messaging, RFC 7807 for HTTP API errors, and ASC 606 / IFRS 15 for revenue recognition. Integration surface includes REST APIs, webhooks, and connectors for Shopify, WooCommerce, NetSuite, and Quickbooks-class systems.

---

## Market Context

The subscription commerce platform market was estimated at roughly USD 10–20 billion in 2025, growing at approximately 15–20% CAGR through 2033 (Data Insights Market, 2025). Incumbent pricing ranges from $40–$100/month at entry level to $10K–$100K+/year for enterprise Zuora or custom Chargebee deployments, with transaction-percentage models common at Recharge and Paddle. Primary buyers are DTC subscription-box ecommerce founders, SaaS CFOs and billing engineers, VPs of Revenue Operations, and finance teams needing ASC 606 compliance.

---

## Project Status

> This project is in the **research and specification phase**.  
> Contributions, feedback, and domain expertise are welcome.

---

## Contributing

We welcome contributions from developers, domain experts, and potential users.
See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

**Important:** All contributions must be your own original work or clearly attributed
open-source material with a compatible licence. Copyright infringement and licence
violations will not be tolerated and will result in immediate removal of the offending
contribution. If you are unsure whether a piece of code, text, or other material is
safe to contribute, open an issue and ask before submitting.

---

## Licence

Licence to be determined. See [discussion](#) for context.
