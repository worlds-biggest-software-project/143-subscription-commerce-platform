# Standards & API Reference

> Project: Subscription Commerce Platform · Generated: 2026-05-03

## Industry Standards & Specifications

### ISO Standards

**ISO 20022 — Financial Messaging Standard**
- URL: https://www.iso20022.org/iso-20022
- Relevance: The global standard for financial data interchange adopted by SWIFT (November 2025), FedNow (July 2025), and payment rails across 70+ countries. Subscription billing platforms interfacing with banking infrastructure for settlement, payouts, and payment reconciliation need to support ISO 20022 message formats. Provides richer, structured remittance data than older wire formats — enabling precise attribution of subscription payments to billing cycles, dunning retries, and partial credits.

**ISO/IEC 27001 — Information Security Management Systems**
- URL: https://www.iso.org/standard/27001
- Relevance: The de facto enterprise security certification for SaaS platforms handling recurring payment data. Subscription platforms store long-lived customer payment method tokens, billing history, and PII across entire subscription lifecycles. ISO 27001 certification (and SOC 2 Type II in the US market) is expected by enterprise buyers and required for integration with corporate procurement systems.

### W3C & IETF Standards

**RFC 6749 — OAuth 2.0 Authorization Framework**
- URL: https://datatracker.ietf.org/doc/html/rfc6749
- Relevance: The authentication standard for all subscription platform integrations: payment gateway APIs (Stripe, PayPal, Adyen), e-commerce platform connectors (Shopify, BigCommerce), accounting systems (NetSuite, QuickBooks), and CRM platforms. Subscription platforms must also implement OAuth 2.0 to enable third-party developers to build integrations on the platform's own API securely.

**RFC 6750 — OAuth 2.0 Bearer Token Usage**
- URL: https://datatracker.ietf.org/doc/html/rfc6750
- Relevance: Defines how OAuth access tokens are transmitted in API requests. Required for all API integrations with payment gateways and e-commerce platforms that subscription billing platforms must connect to.

**RFC 7231 — HTTP/1.1 Semantics and Content**
- URL: https://datatracker.ietf.org/doc/html/rfc7231
- Relevance: Defines HTTP method semantics and status codes for all subscription REST API operations. Critically relevant for idempotency in billing operations — subscription charge endpoints must handle duplicate requests (from network retries) without double-billing subscribers.

**RFC 7807 — Problem Details for HTTP APIs**
- URL: https://datatracker.ietf.org/doc/html/rfc7807
- Relevance: Standardises structured error payloads from REST APIs. Subscription billing APIs must return clear, machine-parseable errors for payment failures, dunning states, invalid billing cycles, and SCA authentication requirements — enabling downstream systems to implement deterministic retry and escalation logic.

**RFC 5988 / RFC 8288 — Web Linking**
- URL: https://datatracker.ietf.org/doc/html/rfc8288
- Relevance: Provides the standard for linking related resources in paginated API responses (e.g., subscription history, invoice lists, payment attempt logs). Relevant for subscription platforms with high-volume billing data requiring cursor-based or offset-based pagination across linked resources.

### Data Model & API Specifications

**OpenAPI Specification 3.1 (OAS 3.1)**
- URL: https://spec.openapis.org/oas/v3.1.0.html ; https://swagger.io/specification/
- Relevance: The industry standard for documenting REST APIs. Stripe, Chargebee, Recurly, Zuora, Paddle, and Recharge all publish OpenAPI/Swagger specifications. OAS 3.1 added native webhook documentation support, enabling subscription platforms to formally document their event schemas (subscription.created, payment.failed, subscription.cancelled) alongside their REST endpoints in a single machine-readable spec.

**JSON Schema 2020-12**
- URL: https://json-schema.org/specification
- Relevance: Standard for validating JSON payloads. Used to validate subscription creation requests, billing configuration objects, webhook event payloads, and dunning rule definitions. Critical for preventing misconfigured billing parameters (invalid intervals, negative amounts, conflicting pricing rules) before they cause silent billing errors.

**CloudEvents Specification (CNCF) — Webhook Event Schema**
- URL: https://cloudevents.io ; https://github.com/cloudevents/spec
- Relevance: CNCF-graduated specification providing a standardised schema and delivery model for event notifications via webhooks, including an HTTP Webhook delivery spec and subscription management API. Subscription platforms publish high volumes of lifecycle events (renewal success, payment failed, subscription paused, churn) to integration partners. Adopting CloudEvents ensures a consistent, versioned event envelope across all event types — enabling integration partners to build unified event handlers without platform-specific parsing logic.

### Regulatory & Compliance Standards

**PCI DSS v4.0 — Payment Card Industry Data Security Standard**
- URL: https://www.pcisecuritystandards.org/document_library/
- Relevance: Mandatory for any subscription platform that stores, processes, or transmits payment card data. PCI DSS v4.0 (with v4.0.1 clarifications) specifically addresses encryption of cardholder data in use — including when stored payment methods (tokenised PANs) are used to bill subscribers in recurring charges. Continuous compliance is now expected annually (not just at audit time). Subscription platforms must also ensure that service providers handling recurring charge processing maintain their own PCI DSS certification.

**PSD2 — EU Payment Services Directive 2 (Strong Customer Authentication / SCA)**
- URL: https://www.eba.europa.eu/regulation-and-policy/payment-services-and-electronic-money/regulatory-technical-standards-on-strong-customer-authentication-and-secure-communication-under-psd2
- Relevance: EU regulation requiring two-factor authentication (SCA) on electronic payments, implemented via 3D Secure 2 (3DS2). For subscription billing: SCA is required only on the first transaction of a recurring subscription; subsequent charges with the same amount to the same merchant are exempt as Merchant-Initiated Transactions (MIT). However, dunning retries following a payment failure may require fresh SCA if the exemption chain is broken. Subscription platforms must model SCA exemptions correctly to avoid false declines and unnecessary authentication friction.

**ASC 606 / IFRS 15 — Revenue Recognition Standards**
- URL: https://asc.fasb.org/606 (ASC 606) ; https://www.ifrs.org/issued-standards/list-of-standards/ifrs-15/ (IFRS 15)
- Relevance: Accounting standards governing when and how subscription revenue is recognised. Under ASC 606 (US GAAP) and IFRS 15 (international), revenue must be recognised when performance obligations are satisfied — not when cash is collected. For subscriptions, this means monthly/annual prepayments must be deferred and recognised ratably over the subscription period. Mid-cycle upgrades, downgrades, and cancellations with partial refunds create contract modification scenarios requiring reallocation of transaction prices. Subscription billing platforms must either produce ASC 606/IFRS 15-compliant revenue schedules or integrate with dedicated revenue recognition modules (Chargebee RevRec, Zuora Revenue).

**GDPR — General Data Protection Regulation (EU 2016/679)**
- URL: https://gdpr.eu/
- Relevance: Subscription platforms process ongoing subscriber personal data throughout the customer lifecycle — signup, billing, payment history, usage, communication preferences, and cancellation. GDPR requires a lawful basis for each processing activity, subscriber consent for marketing communications, data portability for subscriber export, and right-to-erasure workflows that must handle the tension between deletion requests and financial record retention obligations (typically 7 years under accounting law).

**CCPA / CPRA — California Consumer Privacy Act**
- URL: https://oag.ca.gov/privacy/ccpa
- Relevance: Applies to subscription businesses collecting California subscriber data. Subscribers must be able to request deletion of their personal data, opt out of data sale/sharing, and access what data is held. Subscription platforms must implement consumer rights workflows for these requests without breaking billing continuity for active subscribers.

**OWASP API Security Top 10 (2023)**
- URL: https://owasp.org/API-Security/editions/2023/en/0x11-t10/
- Relevance: Defines the most critical API security risks for subscription billing APIs. Particularly relevant: Broken Object-Level Authorization (each subscriber must access only their own account and billing data); Broken Authentication (payment retry and dunning endpoints are high-value fraud targets); Unrestricted Access to Sensitive Business Flows (subscription creation endpoints are abused for trial fraud — creating thousands of free-trial accounts); and Business Logic Abuse (checkout and billing flows must enforce trial limits, coupon constraints, and referral rules that attackers routinely exploit).

### MCP Server Specifications

**Model Context Protocol (MCP) — Agentic Billing Workflows**
- URL: https://modelcontextprotocol.io/ ; https://docs.stripe.com/mcp
- Relevance: MCP is the emerging standard for connecting AI agents to external APIs and data. Stripe has published an official MCP server enabling AI agents (Claude, Cursor, GPT-4) to perform subscription billing operations — creating customers, managing subscriptions, processing payments, and querying invoices — via natural language without custom integration code. The Stripe Agent Toolkit also enables popular agent frameworks (OpenAI Agent SDK, LangChain, CrewAI, Vercel AI SDK) to call Stripe Billing APIs through function calling. Google's Universal Commerce Protocol (UCP, 2026) is built to work with MCP for agentic checkout and post-purchase subscription management. Subscription platforms should expose MCP servers to participate in the agentic commerce ecosystem.

**Universal Commerce Protocol (UCP) — Google Agentic Commerce Standard**
- URL: https://developers.googleblog.com/under-the-hood-universal-commerce-protocol-ucp/
- Relevance: Google's open protocol for agentic commerce, compatible with MCP, Agent2Agent (A2A), and Agent Payments Protocol (AP2). Enables AI agents to complete checkout, manage subscriptions, and handle post-purchase flows (pause, skip, cancel) on behalf of customers across any commerce stack using REST or MCP. Subscription platforms that expose UCP-compatible endpoints will be discoverable to AI shopping agents.

---

## Similar Products — Developer Documentation & APIs

### Stripe Billing

- **Description:** API-first recurring billing integrated within the Stripe payments ecosystem. Covers subscription lifecycle management, flexible pricing plans (flat, metered, tiered), invoicing, customer portal, and webhook events. Also includes an official MCP server and Agent Toolkit for AI agent integrations.
- **API Documentation:** https://docs.stripe.com/api/subscriptions ; https://docs.stripe.com/billing
- **SDKs/Libraries:** Official SDKs for JavaScript/Node.js, Python, Ruby, PHP, Java, Go, .NET — https://docs.stripe.com/libraries
- **MCP Server:** https://docs.stripe.com/mcp
- **Developer Guide:** https://docs.stripe.com/billing/subscriptions/build-subscriptions
- **Standards:** REST/JSON; OpenAPI specification published; webhook events with versioned schemas; PCI DSS compliant payment handling
- **Authentication:** API Key (publishable + secret); OAuth 2.0 for Stripe Connect (marketplace/platform use cases)

### Chargebee

- **Description:** All-in-one subscription management platform for SaaS and recurring commerce. Covers subscription lifecycle, trials, dunning, revenue recognition (ASC 606/IFRS 15 via RevRec module), customer portal, and integrations with 30+ payment gateways and accounting systems.
- **API Documentation:** https://apidocs.chargebee.com/docs/api/
- **Developer Hub:** https://www.chargebee.com/developers/
- **SDKs/Libraries:** Official client libraries for Java, Python, Ruby, PHP, .NET, Node.js, Go — listed at developer portal
- **Developer Guide:** https://apidocs.chargebee.com/docs/api/getting-started
- **Standards:** REST/JSON; HTTP Basic Auth; OpenAPI-documented endpoints; webhook events for lifecycle automation
- **Authentication:** HTTP Basic Auth (API key as username, empty password)

### Recurly

- **Description:** Subscription lifecycle management with ML-powered dunning (Revenue Optimization Engine) for recovering failed payments. Strong revenue operations focus; supports flexible pricing, trials, add-ons, and coupons.
- **API Documentation:** https://recurly.com/developers/api/
- **Developer Hub:** https://recurly.com/developers/
- **SDKs/Libraries:** Python, Node.js, Ruby, PHP, .NET, Java, Elixir — available via GitHub (github.com/recurly)
- **Standards:** REST/JSON; versioned API (current: v2021-02-25); OpenAPI specification; webhook events for subscription and payment lifecycle
- **Authentication:** API Key (HTTP Basic Auth)

### Zuora

- **Description:** Enterprise-grade subscription billing and revenue management with modular architecture. Covers subscription lifecycle, advanced rating engines (usage-based, hybrid), order management, revenue recognition (ASC 606/IFRS 15 via Zuora Revenue), and Zuora Payments for payment processing.
- **API Documentation:** https://developer.zuora.com/
- **API Reference:** https://developer.zuora.com/v1-api-reference/introduction
- **Product Documentation:** https://docs.zuora.com/
- **Standards:** REST/JSON; OpenAPI specification published; SOAP API (legacy); OData for analytics; versioned API releases
- **Authentication:** OAuth 2.0 (client credentials); API key (legacy)

### Paddle

- **Description:** Subscription billing combined with merchant-of-record (MoR) functionality, handling global tax (VAT, GST, sales tax), compliance, and currency for SaaS businesses. Covers subscription lifecycle, checkout, invoicing, and tax reporting across 200+ markets.
- **API Documentation:** https://developer.paddle.com/api-reference/overview
- **Developer Portal:** https://developer.paddle.com/
- **SDKs/Libraries:** Official Python SDK — https://github.com/PaddleHQ/paddle-python-sdk ; TypeScript/Node — https://github.com/kossnocorp/paddle-billing ; PHP, Go per developer portal
- **Developer Guide:** https://developer.paddle.com/
- **Standards:** REST/JSON; OpenAPI specification published; versioned API (version specified in request header); webhook events with signed payload verification
- **Authentication:** API Key; sandbox and live environments with separate credentials

### Recharge Payments

- **Description:** Shopify-native subscription management with flexible subscriber controls (pause, skip, frequency swap). Purpose-built for DTC e-commerce subscription boxes and consumable products. Covers subscription lifecycle, dunning, and analytics.
- **API Documentation:** https://developer.rechargepayments.com/
- **Subscriptions Reference:** https://developer.rechargepayments.com/2021-11/subscriptions/subscriptions_create
- **Standards:** REST/JSON; versioned API (2021-01 and 2021-11); webhook events for subscription and payment events
- **Authentication:** API Key (generated in Recharge merchant admin)

### FastSpring

- **Description:** Global subscription commerce platform acting as merchant of record, handling tax compliance, localization, and multi-currency for software and digital goods businesses. Covers subscription management, checkout, invoicing, and international payment processing.
- **API Documentation:** https://developer.fastspring.com/
- **Standards:** REST/JSON; XML webhook notifications (legacy) and JSON; OpenAPI documentation
- **Authentication:** HTTP Basic Auth (API credentials); webhook HMAC signature verification

### RevenueCat

- **Description:** Mobile-first subscription management platform for iOS (App Store) and Android (Google Play) subscriptions, plus web billing via Stripe and Paddle integration. Covers subscription lifecycle, receipt validation, entitlement management, and cross-platform analytics.
- **API Documentation:** https://www.revenuecat.com/docs/api-v1
- **Developer Docs:** https://www.revenuecat.com/docs/
- **SDKs/Libraries:** iOS, Android, Flutter, React Native, Unity, Cordova, Web SDKs — https://github.com/RevenueCat
- **Standards:** REST/JSON; OpenAPI specification; webhook events for subscription lifecycle
- **Authentication:** API Key (public + secret); platform-specific (App Store Connect, Google Play credentials)

### Lago (Open Source)

- **Description:** MIT-licensed open-source subscription billing and metering platform. Covers subscription lifecycle, usage-based metering, invoicing, and revenue analytics. Self-hosted or managed cloud. Designed as an open-source alternative to Chargebee/Zuora for developers.
- **API Documentation:** https://doc.getlago.com/api-reference/intro
- **GitHub:** https://github.com/getlago/lago
- **SDKs/Libraries:** Ruby gem, Python package, Node.js package, PHP package, Go module — all open source
- **Developer Guide:** https://doc.getlago.com/guide/introduction/welcome
- **Standards:** REST/JSON; OpenAPI 3.0 specification published; webhook events for billing lifecycle
- **Authentication:** Bearer token (API key)
- **Licence:** AGPL-3.0 (self-hosted); commercial licence for SaaS hosted version

---

## Notes

**Stripe's MCP Server as Reference Implementation:** Stripe's official MCP server (docs.stripe.com/mcp) is the most complete example of a billing platform exposing subscription operations to AI agents as of 2026. Subscription platform builders should study this implementation when designing their own MCP server exposure for agentic billing workflows.

**Lago as Open-Source Reference:** Lago (github.com/getlago/lago) is the leading open-source subscription billing platform and provides a useful reference implementation of subscription data models, usage metering, and billing workflows. Its published OpenAPI specification and open-source SDKs make it a practical comparison point for API design decisions.

**SCA / Merchant-Initiated Transaction Complexity:** The interaction between PSD2 SCA exemptions, dunning retry logic, and 3DS2 authentication is one of the most technically complex areas of subscription billing. Platforms must correctly model the MIT (Merchant-Initiated Transaction) exemption chain to avoid SCA false declines on legitimate renewal charges. Stripe's SCA guide (stripe.com/guides/strong-customer-authentication) is the most detailed publicly available treatment of this complexity.

**Revenue Recognition Complexity:** ASC 606/IFRS 15 compliance for mid-cycle subscription changes (upgrades, downgrades, pauses, cancellations with partial credits) requires sophisticated contract modification logic. Most SMB-focused subscription platforms delegate this to the customer's accounting system; enterprise platforms (Zuora Revenue, Chargebee RevRec) provide native revenue recognition automation. This is an underserved area for AI-native automation.
