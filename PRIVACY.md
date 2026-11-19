# Privacy Policy, KIT Apps

_Last updated: 2026-10-26_

KIT Apps is a local-first desktop and web app for turning AI-generated code into runnable apps. It has **no account system and no backend**. Your canvases, code, and files stay on your device (browser `localStorage` or local filesystem). This policy explains the exceptions: anonymous product usage analytics, the licence check that runs only if you have bought the paid tier, and the open-source code KIT Apps downloads from public CDNs to run your apps.

## Summary

- **No personal data.** We do not collect your name, email, IP address, or any of your content (code, canvases, file names).
- **Anonymous, aggregate analytics only.** A small set of named product events (for example "app launched", "canvas saved") with non-identifying properties.
- **On by default for everyone, and anonymous.** Because the data is not personal data, the lawful basis is legitimate interest, not consent.
- **Two ways to stop it:** **Do Not Track / Global Privacy Control** turns analytics off for anyone, at no cost; and an in-app **opt-out switch in Settings** is available on the **paid tier**. Free users always keep the browser-signal path.
- **EU-hosted.** Analytics are processed by PostHog on EU infrastructure.
- **Licence check (paid tier only).** If you activate a licence, KIT Apps sends your licence key and a random machine name to our licence server when you activate and at each launch. Free users send nothing to it.
- **Code from public CDNs.** To run apps, KIT Apps downloads open-source code from unpkg and esm.sh (and from jsdelivr and cdnjs for a packaged or shared copy of the welcome app). The CDN sees your IP address and which file was requested, never your code.
- **No cookies, no cross-site tracking, no ads, no session recording.**

## Who is responsible for this data

The data controller for the processing described in this policy is:

**Metanoia AS**
Organisation number 928 285 898
Kvednanesvegen 49, 4120 Tau, Norway
<support@halison.io>

KIT Apps and the "Halison" / "Halison.io" names are products and brands of Metanoia AS; the legal entity answerable for this data is Metanoia AS.

PostHog acts as our **processor**, processing analytics data on our instruction and not for its own purposes.

## What we collect

When analytics are enabled, KIT Apps sends named product events to understand how the app is used and where people get stuck. The complete event list lives in code (`src/utils/telemetry.js`, the `EVENTS` object) and currently is:

| Event | Non-identifying properties |
|-------|----------------------------|
| `app_launched` | `context` (`desktop` / `web`) |
| `canvas_paste_started` | `has_initial_code` (boolean) |
| `canvas_saved` | `source`, `size` (enum), `total_canvases`, `categorized` (boolean) |
| `canvas_loaded` | `source`, `size` (enum) |
| `canvas_rendered` | none |
| `canvas_render_failed` | none (no error text) |
| `canvas_error_boundary` | `error_hint` (enum category: `syntax` / `dependency` / `compiler` / `crash` / `other`, no error text) |
| `canvas_renamed` / `canvas_duplicated` / `canvas_deleted` | `total_canvases` (count) |
| `canvas_exported` | `size` (enum) |
| `packaging_opened` | none |
| `installer_build_started` | none |
| `installer_build_phase` | `phase` (e.g. `building`) |
| `installer_build_succeeded` | `duration_seconds` |
| `installer_build_failed` | `duration_seconds`, `error_hint` (enum category, no error text) |
| `installer_build_cancelled` | `duration_seconds` |
| `export_png` / `export_pdf` | `paid` (boolean) |
| `share_opened` | `paid` (boolean) |
| `onboarding_completed` | none |

Properties are limited to booleans and short enums. They never contain your code, file names, paths, or any free text. The one exception is a diagnostic report, which is only sent when you ask for it (below).

### Diagnostic reports (only when you send one)

**Help → Submit log to diagnose a problem** sends one `diagnostic_report` event, and only when you click it. It carries:

- a short reference you can quote to us, the app version, `desktop` or `web`, and your browser/WebView user agent;
- the last part of the packaging build log (up to 8,000 characters): timestamps, the tool steps and their output;
- the last 15 canvas renders: time, result, whether it was a component or HTML, the library names it loaded and whether they loaded, and the error message if it failed.

Before it is sent, KIT Apps removes what is yours:

- **Names:** project, canvas and app names, and the file names made from them (the app's `.exe`, the installer, shortcuts, the package folder), become placeholders such as `project-1` and `file-1`. The same name gets the same placeholder within one report.
- **Your user name** in file paths becomes `<user>`.
- **Code:** the source lines a compile error quotes are removed.

An error message can still contain text your app produced itself (for example a message your code throws). If no analytics are configured or you have opted out, nothing is sent; KIT Apps offers a prefilled GitHub issue instead, which you can read and edit before submitting.

## Licence checks (paid tier only)

The paid tier is sold through **Stripe**. **Link** (Stripe's consumer service) is the merchant of record: it handles checkout, payment, tax, receipts, refunds and payment support under its own privacy policy. KIT Apps and Metanoia AS never see your card details.

**Our licence server** (`license.halison.io`, run by Metanoia AS on servers in the EU) turns a purchase into a licence key:

- **When you buy:** Stripe tells the licence server about the purchase. The server stores your licence key, your email address, the subscription's status, and Stripe's ids for your customer record and subscription. It emails the key to you through **Brevo** (our email processor, EU) and shows it on the page you land on after checkout.
- **On activation:** KIT Apps sends the key and a machine name. The machine name is `KIT Apps (<random id>)`; the random id is generated on your device, has no link to your hardware or user account, and only identifies this install as one of the licence's two seats. The server stores it as a seat.
- **At each launch:** KIT Apps sends the key and the seat id. This lets KIT Apps notice a canceled or unpaid subscription, or a seat freed on another machine. If the check cannot reach the server, nothing changes, and paid features keep working offline for up to 30 days after the last successful check.
- **On deactivation** (Settings): KIT Apps sends the key and the seat id, so the seat is freed and deleted.
- **Manage subscription** (Settings): KIT Apps sends the key and the seat id, and the server asks Stripe for a link to Stripe's customer portal, where you cancel or change your card.

The licence server keeps no IP addresses or access logs. It keeps the licence record while your subscription runs and deletes it, with its seats, 90 days after the subscription ends. Nightly backups of the server are kept for 7 days. On your device, KIT Apps stores the key, the seat id and the email address, so Settings can show which licence is active. None of this is added to the analytics events above. Free users make none of these calls.

## Code and media downloaded from public CDNs

To run your apps, KIT Apps downloads open-source code from public content delivery networks (CDNs). These downloads fetch files; they do not send your code, your canvases or your file names, and they carry no analytics.

| What | From | When |
|------|------|------|
| The JSX compiler (Babel) and common libraries (Recharts, lucide-react, prop-types) | `unpkg.com` | When an app that needs them runs |
| Other libraries your app's code imports, and the PNG/PDF export helpers | `esm.sh` | When an app imports a library KIT Apps does not ship, or when you export |
| The welcome animation's player and runtime (HyperFrames) and its animation library (GSAP) | `cdn.jsdelivr.net`, `cdnjs.cloudflare.com` | Only when a copy of the welcome app runs outside KIT Apps, as a packaged app or a share link. KIT Apps itself ships these files. |

What a CDN can see is what any web server sees for a download: your IP address, the time, your browser or WebView user agent, and which file was requested. For libraries your app imports, the file name tells the CDN the name of the library, not your code. Each CDN handles this under its own privacy policy. We receive none of it.

Offline, nothing is downloaded: an app that needs a library it cannot fetch shows an error that says so.

## What we do NOT collect

- No personal data in analytics (name, email, account, device ID).
- **No IP address.** The client nulls the IP before sending, and the project is configured to discard client IP data. No geolocation.
- **No persistent identifier.** Analytics use in-memory storage only (`persistence: 'memory'`), so nothing is written to your device for analytics and there is no stable cross-session ID.
- No autocapture, no page views, no clicks, no session replay, no surveys.
- None of your content (canvas code, HTML, file paths).

## Legal basis (GDPR / ePrivacy)

Because the analytics are cookieless (no information is stored on or read from your device), carry no IP and no identifier, strip your content, and are used only in aggregate to improve the product, the data is **not personal data**. The lawful basis is therefore **legitimate interest** (GDPR Art 6(1)(f)), not consent; there is no personal record to consent to or withdraw. We still give you control: we honor **Do Not Track / Global Privacy Control** for everyone (a no-cost off switch), and the paid tier adds an in-app opt-out in Settings. We do not use the data for advertising, profiling, or automated decisions, and an opt-out only ever reduces collection, it never turns on any identified or persistent mode.

## Processor and data location

Analytics are processed by **PostHog** acting as our data processor, on **EU** infrastructure (`eu.i.posthog.com`). Data is retained for the minimum period needed to spot product trends and is then deleted per the configured retention window.

Purchases are handled by **Stripe**, with **Link** as the merchant of record for the paid tier; their processing of your purchase data is described in their own privacy policies. Licence keys are kept by Metanoia AS on its own licence server in the EU, and the licence email is sent through **Brevo** (EU) as our processor.

## In-app feedback

KIT Apps includes an optional feedback widget. Feedback is **only sent when you explicitly click the submit button**; nothing is collected automatically. When you submit feedback, your message and the current app version are transmitted to **Supabase** (acting as a sub-processor), which stores them on EU infrastructure for Metanoia AS to review.

Feedback submissions may contain personal information you choose to include in your message. The lawful basis is **legitimate interest** (GDPR Art 6(1)(f)): reviewing direct user input to improve the product. Submissions are not linked to your analytics data; the two systems are independent.

To request deletion of a specific submission, write to <support@halison.io>. Because submissions include your message text, we can locate and delete them on request.

## Your choices and rights

- **Browser signal (everyone, free):** enabling Do Not Track or Global Privacy Control disables analytics automatically, on any tier and at no cost.
- **In-app opt-out (paid tier):** open **Settings** (gear icon) and turn **Usage analytics** off. This takes effect immediately and persists. Free users see the disclosure with the switch locked; the browser-signal path above remains available to them.
- Because the data is anonymous and carries no identifier, we cannot link any event back to you, which means we cannot service individual access or erasure requests against it; there is simply no personal record to find. You remain in full control via the opt-out.

## Children

KIT Apps is not directed at children and does not knowingly collect data from them.

## Changes

We will update this document if the data practices change, and note it in the changelog. Material changes are reflected in the in-app notice.

## Contact

For any question about this policy, or to exercise a data protection right, write to <support@halison.io>, or to Metanoia AS, Kvednanesvegen 49, 4120 Tau, Norway.

Questions about the product itself: open an issue on the public repository.
