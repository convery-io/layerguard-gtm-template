# LayerGuard — GTM Tag Template

**Real-time dataLayer validation, bot detection and data quality monitoring for Google Tag Manager.**

> Built by [Buyldoo S.r.l.](https://layerguard.io) — the analytics infrastructure layer for digital agencies and tracking specialists.

---

## What is LayerGuard?

LayerGuard is a data quality monitoring platform that intercepts and validates every dataLayer event directly in the browser — independently of the analytics platform in use (GA4, Adobe Analytics, custom pipelines).

The GTM template allows you to integrate LayerGuard in minutes via Google Tag Manager, without touching your site's source code.

**Key capabilities:**

- ✅ Real-time dataLayer event validation against custom schemas
- 🤖 Bot detection and bot session flagging (`lg_is_bot` cookie)
- 📊 Anomaly detection with automatic email alerts
- 🔒 GDPR-compliant — no PII forwarded by default
- ⚡ Works with any analytics stack (GA4, Universal Analytics, Adobe, custom)

---

## Template Actions

The tag supports three **Action** modes:

### 1. `Load` (initialize SDK)
Loads the LayerGuard SDK (`https://libs.layerguard.io/sdk.js`) and initializes the client with your Stream ID.

| Parameter | Description |
|---|---|
| **Stream Id** | Your LayerGuard stream identifier |
| **Disable anti-bot** | Disables filtering of known bot sources (e.g. Search Console crawlers) |
| **Flag bot sessions** | Stores bot status in the `lg_is_bot` cookie based on a configurable score threshold |
| **Anti Bot threshold** | Score threshold (0–100) above which a session is flagged as bot. Default: 70 |
| **Anonymization Triggers** | Comma-separated list of field names to anonymize before sending to collection servers |

**Recommended trigger:** All Pages — once, on `gtm.js` or DOM Ready.

---

### 2. `Send Event` (validate and track)
Validates a dataLayer event against a configured model and sends it to LayerGuard for monitoring.

| Parameter | Description |
|---|---|
| **Event Validation Model** | The model ID configured in your LayerGuard dashboard |
| **Analytics Event Name** | The GA4 / analytics event name (e.g. `add_to_cart`) |
| **Event Settings Variable** | Optional: a GTM Event Settings variable to inherit shared parameters |
| **Event Params** | Key/value pairs of event parameters to validate |

**Recommended trigger:** Custom event triggers matching each event you want to monitor (e.g. `purchase`, `add_to_cart`, `generate_lead`).

---

### 3. `Update` (update session context)
Updates the active LayerGuard session context (e.g. after consent changes or user identification).

---

## Installation

### Via GTM Template Gallery (recommended)

1. In GTM, go to **Templates → Tag Templates**
2. Click **Search Gallery**
3. Search for **LayerGuard**
4. Click **Add to workspace**

### Manual import

1. Download [`template.tpl`](./template.tpl) from this repository
2. In GTM, go to **Templates → Tag Templates → New**
3. Click the three-dot menu (⋮) in the top right → **Import**
4. Select the downloaded file and click **Save**

---

## Quick Start

### Step 1 — Initialize LayerGuard

Create a new tag using the LayerGuard template:

- **Action:** `Load`
- **Stream Id:** your stream ID from the [LayerGuard dashboard](https://app.layerguard.io)
- **Trigger:** All Pages (once, on `gtm.js`)

### Step 2 — Validate events

For each event you want to monitor, create a second tag:

- **Action:** `Send Event`
- **Event Validation Model:** the model ID from LayerGuard
- **Analytics Event Name:** the event name (e.g. `purchase`)
- **Event Params:** map your dataLayer variables to the expected parameters
- **Trigger:** the corresponding GTM trigger

### Step 3 — Verify in LayerGuard

Open your LayerGuard dashboard and browse to the **Live Events** section. Fire a test event on your site and confirm it appears with the correct validation status.

---

## Bot Detection

When the **Flag bot sessions** option is enabled, LayerGuard evaluates a behavioral score for each session. Sessions scoring above the configured threshold are flagged by setting the `lg_is_bot` cookie.

You can use this cookie as a GTM variable to:
- Exclude bot traffic from your analytics tags
- Pass bot status as a custom dimension to GA4
- Block or throttle server-side forwarding

---

## GDPR & Privacy

LayerGuard is designed with privacy compliance in mind:

- The SDK does not collect or forward Personally Identifiable Information (PII) by default
- The **Anonymization Triggers** parameter allows you to declare field names that must be masked before transmission
- The tag reads `analytics_storage` consent state via GTM's Consent API
- No third-party cookies are set without user consent

---

## Links

- 🌐 **Website:** [https://layerguard.io](https://layerguard.io)
- 📖 **Documentation:** [https://buyldoo.gitbook.io/layerguard](https://buyldoo.gitbook.io/layerguard)
- 📩 **Support:** [info@layerguard.io](mailto:info@layerguard.io)
- 🏢 **Developed by:** [Buyldoo S.r.l.](https://layerguard.io) — a Convery.io company

---

## License

Apache 2.0 — see [LICENSE](./LICENSE)

Copyright 2025 Buyldoo S.r.l.
