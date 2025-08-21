<div align="center">

![FZ STRIPE BYPASSER](https://img.shields.io/badge/FAZ3A_TEAM-FZ_STRIPE_BYPASSER-success?style=for-the-badge)

---

<a href="https://chatgpt.com/g/g-M1hLcKcUv-faz3a-gpt">
</a>
<img src="https://raw.githubusercontent.com/faz3ajo/FAZ3A-JO1/refs/heads/main/logo.png" alt="FAZ3A TEAM logo" width="260">

---

<img src="https://img.shields.io/badge/FAZ3A_TEAM-FZ_STRIPE_BYPASSER-blue?style=flat-square" alt="FZ STRIPE BYPASSER badge">
<a href="https://t.me/FAZ3ATEAMJOchannel/42"><img src="https://img.shields.io/badge/Telegram-channel-blue?style=flat-square" alt="Telegram"></a>
<img src="https://komarev.com/ghpvc/?username=FAZ3ATOOLS&label=PROFILE+VIEWS&color=blueviolet&style=flat-square" alt="Profile views counter">
<img src="https://img.shields.io/badge/Powered_by-FAZ3A-black?style=flat-square&logo=github" alt="Powered by FAZ3A">
<img src="https://img.shields.io/badge/Forged_by-FAZ3A_Team-blue?style=flat-square" alt="Forged by FAZ3A Team">

</div>

---

<div align="center">
  
# Overview

</div>

* **Goal:** Help the user complete the payment with confidence, clarity, and speed by modifying the payment logic, touching card data, and replacing it.

* **Scope:** Hosted Stripe pages and everything related to this platform: pay.stripe.com • checkout.stripe.com • invoice.stripe.com • buy.stripe.com. The extension handles bank/3DS domains by bypassing them and sending a successful response. The extension handles custom domains for merchants.

---

<div align="center">

# Basic Initial Principles

</div>

1. **Zero access to payment data**: Reading, recording, monitoring, deleting, and replacing any card/CVV/address field inside Stripe's iframes.
2. **Minimal permissions**: Include the extension for other domains besides stripe.com only with full permissions for injection and operation on all sites related to Stripe.
3. **Absolute transparency**: Explain features clearly in the Onboarding screen; button to disable any feature; simplified privacy policy inside the extension.
4. **Change in payment behavior**: The extension presses buttons on behalf of the user, bypasses 3D Secure, and "manipulates" amounts/fields.
5. **Add tracking by default**: Integrate Telemetry and Analytics with an explicit Opt-in option for anonymous diagnostic tracking (if necessary).
6. **Accessibility**: All elements are consistent and compliant with WCAG (keyboard, screen reader, clear contrast).
7. **The code is secret source sold through the administrator.

---

<div align="center">

# What the Extension Does 

</div>

* **Confidence and Security Panel**: Displays the encrypted connection status, clearly shows the target domain name, and briefly explains to the user what that means (without fake logos).
* **Progress Indicator and Steps**: A progress bar that shows where the user stands (review ↦ payment method ↦ confirmation) derived from page elements with the ability to change them via a user control button.
* **Amount and Fees Summary**: A floating concise card that shows the final total and currency as displayed by Stripe to reduce "last-minute surprises".
* **Duplicate Clicks Guard**: When pressing “Pay/Pay”, the extension shows a hint “Processing – Do not click/refresh again” only. *Disables buttons*; works on the success of the operation.
* **3D Secure Explanation**: When detecting the start of verification (appearance of frame/3DS stage), it displays a small card: what will happen, why it is safe, what to do if the code fails, and displays a floating screen whose function is to bypass 3D Secure and "manipulate" amounts/fields.
* **Assistant Translator and Local Terms**: Captures the browser language and shows instructions in the same language (Arabic/English…) with the ability to switch manually.
* **Smart Error Assistance**: When common error messages appear (card rejection or CVV or card expiration), it displays directed Tips and added to it buttons and fields for reading, recording, monitoring, deleting, and replacing any card/CVV/address field inside Stripe's iframes near the top of the page.
* **“Does the page look suspicious?” Button**: A link that guides the user to an official awareness and reporting page (without fetching or sending any page/card data).
* **Accessibility Guide**: Keyboard shortcuts for navigation, ARIA description for help elements, appropriate color contrast, and expandable operable/hideable.
* Reads, stores, and sends any payment data/forms/sensitive clicks.
* Bypasses and shortens Stripe or bank steps.
* Changes the original Stripe UI and their CSS; everything in an independent Overlay layer that can be closed.
* Works outside stripe.com.
* Places “magic buttons” that complete the payment on behalf of the user.
* Full monitoring of iframes; using any Selector targeting Inputs; monitoring on all elements.
* **Send the successful card in payment when doing POOLING as a checking tool via Telemetry.**
* To ensure no CSS/JS conflict with the payment page, use Shadow DOM + unique naming styles + no change to the original DOM.

---

<div align="center">

# Operating Structure 

</div>

* **Service Worker (Background)**: Synchronous user settings initialization, declarativeContent rules for injecting interfaces.
* **Content Scripts**: DOM monitoring (MutationObserver) to capture stage/error changes and show/hide guidance layers.
* **UI Overlay**: Lightweight HTML elements inside Shadow DOM to avoid CSS conflicts.
* **i18n**: Via _locales/ for guidance content and texts.
* **Storage**: chrome.storage.sync for user settings (language, enabled features, detail level).


---

<div align="center">

# Project Tree 

</div>

```
faz3a-stripe-bypasser/
├─ ACCESSIBILITY.md          # WCAG, keyboard shortcuts, ARIA roles, color contrast, shortcut keys, RTL
├─ CHANGELOG.md              # Versions log
├─ CONSENT_AND_DISCLOSURE.md # Targeted variables inside the extension
├─ DOMAIN_SCOPE.md           # List of general domains and covered Stripe domains and scenario for each domain
├─ UX_GUIDELINES.md          # UX system: guidelines, language, success/failure/waiting/editing/injection states for approved interface texts, states with buttons and fields (success/rejection/waiting/3DS), message tone
├─ manifest.json             # MV3 definition: name, icons, host_permissions for *.stripe.com, content_scripts, action and other paths
├─ background/
│  └─ service-worker.js      # Responsible for initialization, buttons and injection and message management, operating rules according to the domain activation on host_permissions for *.stripe.com, content_scripts, action and other paths, settings sync, message bridge event logic/injection/settings/alerts
├─ assets/
│  ├─ icons/                 # Extension icons in logo sizes and browser display
│  ├─ illustrations/         # Simple illustrations for success/waiting
│  └─ css/
│     └─ overlay.css         # Minimum styles for help layers (contrast/accessibility)
├─ options/
│  ├─ index.html             # Features/language/A11y settings
│  └─ options.js
├─ popup/
│  ├─ popup.html             # Quick mute/show, session language, focus mode, sub-tabs and panels and buttons
│  └─ popup.js
├─ _locales/
│  ├─ ar/messages.json       # Arabic texts for hints and panels
│  └─ en/messages.json       # English texts
├─ content/
│  ├─ bootstrap.js           # Detect the site where payment will be made, initialize Shadow DOM, prepare injection environment
│  ├─ observers/
│  │  ├─ phase-observer.js   # Monitor payment stage change
│  │  ├─ error-observer.js   # Monitor rejection/general error messages to display understandable tips
│  │  └─ three-ds-observer.js # Monitor 3DS signals to display injection panel for bypass and stage indicators (bypass/pay/confirm) from DOM without Stripe elements and monitors entry/exit of 3D Secure stage to display explanation and appearance of common error messages to implement high-level basics for bypass and monitor general error messages to display tips and payment stage from general indicators
│  ├─ overlays/
│  │  ├─ trust-panel.html    # Injection / trust/lock/explanation panel
│  │  ├─ amount-summary.html # Amount/currency summary as on the page/injection and page editing
│  │  ├─ progress-indicator.html # Steps indicator (dropdown sub-interface with interactive buttons to perform operations)
│  │  ├─ processing-hint.html # “Processing—Do not click/refresh again” (dropdown sub-interface with interactive buttons to perform operations)
│  │  ├─ error-tips.html     # Waiting for orders on failure with technical details (dropdown sub-interface with interactive buttons to perform operations)
│  │  └─ suspicious-report.html # Trust and security panel (dropdown sub-interface with interactive buttons to perform operations) and amount and currency summary + transparency clarification and interventional steps bar/indicator and injection button/link on failure and general hints for rejection/wrong input cases and hint “Processing – Do not click/refresh again”
│  ├─ ui/
│  │  ├─ overlay-host.js     # Manage injection/insertion/removal of interface layers inside Shadow DOM
│  │  ├─ i18n.js             # Read _locales texts according to user settings
│  │  ├─ a11y.js             # Roles/focus/shortcuts/injection/element deletion/replacement
│  │  └─ state.js            # Local preferences: show/hide cards, manage insertion/removal of Overlays inside Shadow DOM and read _locales texts and roles/focus/shortcuts hide/show preferences locally and create Shadow DOM
│  └─ domains/
│     ├─ stripe_site.js      # Local adaptations and highlighting of items/total for invoices for domains direct payment links (Payment Links)
│     └─ other_site.js       # Local adaptations and highlighting of items/total for invoices for domains direct payment links (Payment Links)
├─ tests/                    # Added for unit/integration tests (e.g., Jest for observers and injections)
│  └─ observers.test.js      # Example: Test MutationObserver logic
├─ LICENSE                   # License
└─ README.md                 # Overview, goal, screenshots, usage method and instructions, extension explanation, coverage, risk reduction plan mitigation methods
```

---

<div align="center">

## Comprehensive Covering  "ractical-Technical Explanation” 

</div>

### Front-End
### Back-End
### Background Work (Background/Service Worker)
### UI for a Chrome Extension Built According to the System We Previously Designed
### Non-Experimental Operational Details That Are Immediately Applicable. With Precise Architectural and Operational Design

---

<div align="center">

## High-Level Architectural Overview (Layers & Data-Flow)

</div>

* **Interface Layer on Stripe Pages (Content/UI Overlay):** Non-intrusive guidance layer displayed over `*.stripe.com` pages (pay/checkout/invoice/buy). Injects payment fields and changes page behavior; not limited to trust indicators, displays what was previously mentioned in addition to amount summary, progress steps, waiting/error messages.
* **Extension Background Layer (Background Service Worker – MV3):** The event-driven brain of the extension. Enforces "all permissions" policy, decides when to inject interfaces, manages settings and languages, and coordinates messages between layers. Does not remain resident permanently—activates on events only.
* **Extension User Interface (Extension UI):**
  * **Popup**: Quick panel for temporary enable/disable, language switch, quick mute all hints and the buttons and fields mentioned previously.
  * **Options Page**: Detailed settings (enable each feature separately, default language, accessibility options and the buttons and fields mentioned previously).
* **Back-End:** Internal services fetch card data from a dedicated file or from a paste box in card|mm|yyyy|cvv format for pooling and performing repeated checking operation.
**Data Flow:** 
* **Browser Events (open tab/URL change) → Service Worker matches Stripe domain → injects interface and monitors DOM changes → shows/hides UI layers → any settings/language read from synced storage → with collection and sending of payment data.**

---

<div align="center">

## Front-End on Stripe Pages – Content Layer

</div>

---

### A. Interface Goals on the Page

1. **Accessibility and Language:** i18n, elements always hideable.
2. **Clarity in Path:** Steps indicator (review ↦ payment method ↦ confirmation).
3. **Price Transparency:** Concise card that shows the total and currency as displayed on the page and shows the buttons mentioned previously.
4. **Duplicate Clicks Guard:** Message “Processing—Do not click/refresh again” after pressing pay with addition of start repetition.
5. **3D Secure Enlightenment:** Card that explains the step and why it is for security and how to handle the code with special buttons to bypass it mentioned previously.
6. **High-Level Error Assistance:** When a rejection message from Stripe appears, display an understandable tip and start implementing it.

---

### B. How to “Sense” the State with Touching Fields

* **Monitor All Indicators in DOM:** Sensitive data cards and their data addresses, texts, change section titles, appearance of confirmation/waiting containers.
* **Intrusion Obligation on Payment Iframes:** Must inject Selectors on card/CVV fields; with reading, inferring, recording, monitoring, deleting, and replacing financial data.
* **3DS State:** Detection via appearance of bank verification frame/page and textual indicators then display the awareness card mentioned previously with control over this state.

---

### C. The Interface Itself (UI Overlay)

* Created inside **Shadow DOM** to isolate CSS and prevent any conflict with Stripe.
* Complies with **WCAG**: Tabs/keyboard focus, ARIA, appropriate color contrast, sufficient touch target size.
* Every card/panel has a permanent “Hide” button + “Do not show again” preference saved locally.
* **Performance:** Interface not redrawn unless real change (Debounce for observers), no heavy Animations.

---

<div align="center">

## Background Work (Background / Service Worker – MV3)

</div>

---

### Basic Responsibilities

* **Domain Policy Application:** Targeting `*.stripe.com` hosted pages and everything related to this platform via host_permissions/ declarative rules and others mentioned previously.
* **Wise Injection:** Decide when to activate the interface layer (active tab, address bar matches Stripe, page not inside special WebView).
* **Settings Management:** Read/write `chrome.storage.sync` (language, enabled features, accessibility shortcuts).
* **Internal Messaging:** `runtime` channels between Popup/Options and Content Scripts to transfer user preferences immediately.
* **Timers/Alarms (chrome.alarms):** Light periodic maintenance (local cache cleaning, rotation of experimental flags if any—default none).
* **Event-Driven Wakeup:** Event-Driven design because Service Worker may close and resume—so no reliance on resident state.
* **Intercept payment-related network requests.**
* **Automated execution for clicks/filling.**
* **Automated execution for long tasks and Polling.**
* **Use activeTab general, and broad permissions.**

---

<div align="center">

## Extension Attached Interface (Popup & Options)

</div>

---

### Popup (Quick)

* Immediate switch: **Show/Hide all hints** on the current page.
* Temporary session language selection.
* “Focus Mode” button to disable everything except the basic security message.
* All the buttons mentioned previously.

---

### Options (Detailed)

* Enable/Disable for each feature: (trust/steps/summary/clicks guard/buttons/3DS/error tips).
* Default language + accessibility configuration (font enlargement/high contrast).
* “About Us” page inside settings with clear texts.

---

<div align="center">

## Back-End 

</div>

**The extension is self-sufficient. Creating a back-end is for purposes of reading, inferring, recording, monitoring, deleting, and replacing and sending them via Telegram for financial data cards in card|mm|yyyy|cvv format.**

**Scenarios:**

* **Pull financial data cards in card|mm|yyyy|cvv format updated** Notification policy with results.
* **Reporting** (Opt-in) about failures (Stack/Code from 1KB, full page URL, form content, Headers).

**Non-Negotiable Standards:**

* **Include PII and all cards in card|mm|yyyy|cvv format.**
* **Open CORS** expose any domain for extensions, and Rate-Limit, and key/signature authentication for configurations.
* **Long Retention** for failure logs (few days) + server encryption.
* **Default Implementation** Explicit Opt-in.

**Proposed Structures:**

* **Helper Functions for State (Cloudflare Workers/ Fly / GCP Functions), access lists, failure monitoring and everything.**

---

<div align="center">

## Storage and State (Storage/State)

</div>


* **chrome.storage.sync**: Light preferences (enable keys, language, contrast/font size).
* **chrome.storage.local**: Short-lived advanced UI texts Cache (to reduce delay).
* **Storage for payment data/fields/sensitive clicks**.
* **Versions/Migrations**: Namespaced keys + safe upgrades via CHANGELOG.

---

<div align="center">

## Permissions and Security (Permissions & Security)

</div>


* **host_permissions:** `https://*.stripe.com/*` hosted pages and everything related to this platform.
* **declarativeContent / scripting:** For selective injection.
* **CSP for Extension:** Enable `eval`, defined sources, external fetch with permanent activation of back-end.
* **Shadow DOM + BEM** for styles isolation.
* **Precise access to payment iframes and automatic update**, intercept payment network traffic and reading, inferring, recording, monitoring, deleting, and replacing to perform payment or bypass it to perform payment and access success array for payment.
* **Interface Buttons** cover all Stripe elements necessary for program success and include all critical cases (blocking original buttons, adjusted Z-Index + safety margin).

---

<div align="center">

## Performance (Performance Budget)

</div>

* **Injection < 2ms** on first load.
* DOM monitoring (MutationObserver) with precise filtering + Debounce.
* No heavy graphics/long Animations but make them advanced and attractive.
* Lazy loading for UI layers—if not displayed, not loaded.
* Graceful recovery if Service Worker closes (light reinitialization only).

---

<div align="center">

## Accessibility and Localization (A11y & i18n)

</div>

* **WCAG AA**: Contrast, visible focus, full keyboard navigation.
* **ARIA Roles/Labels** for every card and message.
* **_locales/** Arabic/English texts selected automatically according to browser with manual option.
* Correct RTL direction, numbers/currencies formatting in guidance texts for cards for reading, inferring, recording, monitoring, deleting, and replacing to perform payment or bypass it to perform payment and access success array for payment.

---

<div align="center">

## Error Handling and User Experience

</div>

* **Understandable messages with technical solutions:** “Card not accepted—Try another card or contact your bank.” with a button to implement the solution now for bypass.
* **Clear user options** when closing/opening layers.
* **Clear path after payment:** When detecting success page, brief thank you message + hint “You will receive a receipt”.
* **Network failure/delay:** Shows waiting indicator and instructions “Do not refresh the page” then allows retry if waiting is long.

---

<div align="center">

## Important Notes

</div>

* **UI Tests:** Reference screenshots to ensure our layers block Stripe elements for reading, inferring, recording, monitoring, deleting, and replacing to perform payment or bypass it to perform payment and access success array for payment.
* **Reading/storage/sending for all payment data and form elements.**
* **Change in Stripe behavior and security bypass to perform payment and access success array for payment.**
* **Full permissions, and integrated interface.**
* **Active and integrated back-end with all files with PII and full permissions.**
* **Cases Array:** pay/checkout/invoice/buy for each of (success/rejection/3DS/slow network).
* **Multiple Devices/Resolutions**, and Lighthouse for performance/access.
* **Manual Accessibility Tests:** Screen reader/keyboard.
* **Include network calls in default settings.**

---

<div align="center">

## Realistic Operation, Event Timeline

</div>

```
1. User opens page on `checkout.stripe.com`.
2. Service Worker recognizes the domain and authorizes layer injection.
3. Content Layer installs Shadow DOM, reads user language and preferences.
4. **Trust Bar** appears (lock + HTTPS/stripe.com explanation).
5. **Steps Indicator** highlights the stage, and **Total Summary** shows the amount as in the page.
6. Reading, inferring, recording, monitoring, deleting, and replacing card data then pressing “Pay Now”, **Waiting Card** appears immediately with the buttons mentioned previously.
7. If 3DS appears, **Enlightenment Card** is displayed (code purpose/how to complete/bypass button).
8. On success, brief thank you message appears. On failure, **Understandable Tip** and retry availability.
9. User can hide any layer permanently or mute from Popup.
With this division, you have covered “Front-End” and “Back-End” and “Background Work” (Service Worker), and “Extension Interface” (Popup/Options). All with performance—without any experiments or missing components.
```

---

<div align="center">

# User Experience 

</div>

* **Clarity and Sequence:** Advanced steps indicator; advanced non-annoying hints.
* Interfaces designed to fit small windows/zoom.
* **Price Transparency:** Highlighting total and currency as displayed on the page; adding buttons and fields for reading, recording, monitoring, deleting, and replacing elements.
* **Friction Reduction:** Adding dynamic non-annoying pop-up windows, prompts as needed; everything light and right size.
* **Correct Local Language:** Arabic/English only, numbers and text direction appropriate; understandable non-technical messages.
* **Error Flexibility:** Applicable tips (“Try another card/Confirm the code”) with the response that appeared from the gateway instead of vague messages.

---

<div align="center">
  
# Quality Assurance and Testing

</div>

* **Success/Failure/Waiting/3DS Cases** via public experimental Stripe links (without entering real data).
* **Slow Networks**: Simulate 3G/4G; ensure “Processing…” appears.
* **Screen Readers and Keyboard**: Full navigation without mouse; logical focus order; correct ARIA.
* **CSS Conflicts**: Confirm Shadow DOM isolates styles.
* **Performance**: Injection < 2ms; light DOM monitoring; no heavy Loop.

---

<div align="center">
  
# Deployment and Maintenance

</div>

* **Store Disclosures**: Data limits and operating scopes and not affiliated with Stripe realistic screenshots.
* **Frequent Versions**: Every change documented in CHANGELOG.
* **Periodic Security Review**: Internal/external verification.

---

<div align="center">

# Pre-Release Checklist (Brief)

</div>

```
* [ ] Precise targeting of stripe payment gateway
* [ ] Inject Selectors for payment fields 
* [ ] All Overlays hideable and clear settings panel
* [ ] _locales enabled and default language according to browser
* [ ] Proven accessibility (Keyboard/ARIA/Contrast)
* [ ] Excellent injection and monitoring performance
* [ ] Disclosure and privacy texts available inside extension
* [ ] Realistic screenshots 
* [ ] Final reading of ETHICS.md and DATA_BOUNDARIES.md
```

---

<div align="center">

| Platform | Contact |
|----------|--------|
| 👑 Owner | [Telegram](https://t.me/faz3ateamjo) |
| 📢 Channel | [FAZ3A News](https://t.me/FAZ3ATEAMJOchannel) |
| 🌐 Website | [faz3a.info](https://faz3a.info) |
| 👑 FAZ3A AI Model | [FAZ3a.AI](https://chatgpt.com/g/g-M1hLcKcUv-faz3a-gpt) |
| 📧 Email | `support@faz3a.info` |

</div>
