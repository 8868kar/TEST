# Cynbit Website — Comprehensive Bug & Issue Report

**Target:** [https://www.cynbit.in/](https://www.cynbit.in/) | **Date:** 2 November 2026 | **Tester:** Kartik Karnwal  
**Testing Methodology:** Live multi-device interactive browser execution (Chromium Desktop, Mobile, Tablet Emulation, HTTP Protocol Analysis).  
**Evidence Archive:** Screen captures and session recordings stored in `evidence/`.

---

## 1. Executive Issue Summary

| Severity | Definition | Count |
|---|---|:---:|
| **Critical** | Core flow unusable; immediate data loss; zero fallback | **0** |
| **High** | Major functional defect; serious compliance/privacy violation; broken input processing | **3** |
| **Medium** | Notable usability, SEO dilution, missing security headers, or trust degradation | **14** |
| **Low** | Cosmetic glitches, minor copy discrepancies, or non-blocking polish | **11** |
| **Total Logged Defects** | | **28** |

---

## 2. Master Bug Index

| ID | Title | Category | Severity | Priority | Verification Status |
|---|---|---|:---:|:---:|:---:|
| **CYN-001** | Blog lacks page controls; query params `?page=0`/`?page=1` do not page content | Functional | Low | P3 | **Verified in Browser** |
| **CYN-002** | Contact page "Our impact" CTA button links to `/case-studies` instead of `/impact` | Usability | Low | P3 | **Verified in Browser** |
| **CYN-003** | Phone numbers and contact emails conflict between footer and Contact page | Content / Trust | Medium | P2 | **Verified in Browser** |
| **CYN-004** | Careers application form demands excessive personal data (DOB, Gender, WhatsApp, Address) | Privacy / Compliance | **High** | P1 | **Verified in Browser** |
| **CYN-005** | Google Analytics declared in cookie policy but zero cookie consent banner is rendered | Privacy / Compliance | **High** | P1 | **Verified in Browser** |
| **CYN-006** | Typo "Unheared Stories" in the `/diaries` main H1 heading | Content / Branding | Low | P3 | **Verified in Browser** |
| **CYN-007** | Copy errors: "Lead by Mohak Saini", comma capitalization, unpunctuated services H1 | Content | Low | P3 | **Verified in Browser** |
| **CYN-008** | Route-specific titles and meta missing; subpages inherit homepage title; double `&amp;` | SEO | Medium | P2 | **Verified in Browser** |
| **CYN-009** | Title tag template duplicates brand (`... | Cynbit Technologies | Cynbit Technologies`) | SEO | Low | P3 | **Verified in Browser** |
| **CYN-010** | `og:url` declares apex domain `https://cynbit.in` across all pages while site runs on `www` | SEO | Medium | P2 | **Verified in Browser** |
| **CYN-011** | Social share image `og:image` is configured as SVG (`logo.svg`) | SEO / Social Cards | Low | P3 | **Verified in Browser** |
| **CYN-012** | Conflicting statistics: 99.99% vs 99.9% uptime, 100+ projects vs 13 case studies | Content / Credibility | Medium | P2 | **Verified in Browser** |
| **CYN-013** | Unverifiable metric claims and fake "live" badges ("Efficiency 95%", "Status 100%") | Usability / Trust | Medium | P2 | **Verified in Browser** |
| **CYN-014** | Placeholder avatars loaded from `i.pravatar.cc` and stock photos hotlinked from Unsplash | Content / Privacy | Medium | P2 | **Verified in Browser** |
| **CYN-015** | `next/image` generates oversized requests (`w=3840`) for tiny icon/avatar elements | Performance | Medium | P2 | **Verified in Browser** |
| **CYN-016** | Team member bios swapped between Co-Founder and CTO | Content | Low | P3 | **Verified in Browser** |
| **CYN-017** | Material Symbols ligature names (`east`, `expand_more`, `arrow_forward`) leak into DOM text | Accessibility (a11y) | Medium | P2 | **Verified in Browser** |
| **CYN-018** | Full multi-line paragraph marked up as `<h2>` on `/bitelevate/paths` | Accessibility (a11y) | Low | P3 | **Verified in Browser** |
| **CYN-019** | Product CTA buttons ("Start Building Legacy", "Audit Reputation") lack clear destination | Usability | Medium | P2 | **Verified in Browser** |
| **CYN-020** | Service CTAs ("Inquire", "Start discovery", "Roadmap") lack explicit hyperlink anchors | Functional / Usability | Medium | P2 | **Verified in Browser** |
| **CYN-021** | "Drop a portfolio" CTA directs users to `/contact` form with no file attachment capability | Usability | Low | P3 | **Verified in Browser** |
| **CYN-022** | Stale and ambiguous date formats ("Student diaries 2025" vs footer 2026; "Apr 26") | Content | Low | P3 | **Verified in Browser** |
| **CYN-023** | Blog category filter buttons do not match article tag taxonomy | Functional / Usability | Low | P3 | **Verified in Browser** |
| **CYN-024** | Newsletter signup form lacks explicit opt-in consent checkbox | Privacy / Compliance | Medium | P2 | **Verified in Browser** |
| **CYN-025** | Company timeline on `/story` has chronological jumps (2024 to 2022 with missing 2023) | Content | Low | P3 | **Verified in Browser** |
| **CYN-026** | Contact form fails silently on empty submission and invalid email without inline feedback | Functional / UX | **High** | P1 | **Verified in Browser** |
| **CYN-027** | Lack of a "Skip to Content" link for keyboard and screen reader accessibility | Accessibility (a11y) | Medium | P2 | **Verified in Browser** |
| **CYN-028** | Critical security headers missing: CSP, X-Frame-Options, X-Content-Type-Options | Security | Medium | P2 | **Verified via HTTP Header Audit** |

---

## 3. In-Depth Bug Profiles & Reproduction Steps

---

### CYN-026 — Contact Form Submits Silently Without Inline Error Feedback
* **Severity:** **High** | **Priority:** **P1** | **Category:** Functional / UX | **Confidence:** Verified in Browser
* **Target URL:** `https://www.cynbit.in/contact`
* **Evidence:** `evidence/contact_form_validation_1793615961686.png`
* **Steps to Reproduce:**
  1. Navigate to `https://www.cynbit.in/contact`.
  2. Click the "Send Transmission" / "Submit" button with empty fields.
  3. Enter Name: "Test User" and Email: "invalid-email" and click Submit.
* **Actual Result:** The page executes no visual response; no inline error states (e.g., "Please enter a valid email address", "This field is required") are displayed near the inputs. The user receives zero feedback on whether the transmission failed or succeeded.
* **Expected Result:** Clear inline validation messages highlighting defective inputs, with aria-invalid tags and focus placed on the first invalid field.
* **Remediation:** Implement Zod / React Hook Form client-side validation with explicit `<span role="alert" className="error-text">` notifications and standard HTML5 input type enforcement.

---

### CYN-004 — Careers Application Form Demands Excessive Personal Data
* **Severity:** **High** | **Priority:** **P1** | **Category:** Privacy / Compliance | **Confidence:** Verified in Browser
* **Target URL:** `https://www.cynbit.in/careers/qa-testing-intern`
* **Evidence:** `evidence/careers_page_1793616081487.png`
* **Steps to Reproduce:**
  1. Navigate to `/careers/qa-testing-intern`.
  2. Inspect the required application input fields.
* **Actual Result:** Mandatory fields include Date of Birth, Gender, WhatsApp number, Permanent Residential Address, and Notice Period for a student/entry-level internship. This directly contradicts the Cynbit Privacy Policy §1 ("we only collect minimal personal information... typically name, email, and professional context").
* **Expected Result:** Minimize initial candidate screening data to Name, Email, Phone, Resume Link, and Portfolio.
* **Remediation:** Remove Date of Birth, Gender, and Permanent Address from initial form steps. Link the Privacy Policy on the consent submission checkbox.

---

### CYN-005 — Google Analytics Declared in Policy but Cookie Consent Banner Missing
* **Severity:** **High** | **Priority:** **P1** | **Category:** Privacy / Compliance | **Confidence:** Verified in Browser
* **Target URL:** Global / `https://www.cynbit.in/`
* **Evidence:** `evidence/cynbit_homepage_desktop_1793615340730.png`
* **Steps to Reproduce:**
  1. Open a clean browser profile / incognito window.
  2. Visit `https://www.cynbit.in/`.
  3. Inspect Cookies and LocalStorage.
* **Actual Result:** The Cookie Policy explicitly specifies that third-party analytics (Google Analytics) are set on user devices. However, no cookie consent banner, acceptance dialogue, or opt-in selector is rendered to visitors.
* **Expected Result:** A compliant consent banner allowing users to Accept / Reject non-essential analytics cookies before any tracking scripts execute (DPDP Act / GDPR compliance).

---

### CYN-028 — Missing Critical HTTP Security Headers & Wildcard CORS
* **Severity:** **Medium** | **Priority:** **P2** | **Category:** Security / Architecture | **Confidence:** Verified via Protocol Scan
* **Target URL:** `https://www.cynbit.in/`
* **Header Analysis:**
  ```http
  Strict-Transport-Security: max-age=63072000
  Access-Control-Allow-Origin: *
  ```
* **Vulnerabilities Identified:**
  1. **No Content-Security-Policy (CSP):** Exposes visitors to cross-site scripting (XSS) and unsafe script injections.
  2. **No X-Frame-Options / frame-ancestors:** Cynbit pages can be embedded within third-party `<iframe>` elements for clickjacking campaigns.
  3. **No X-Content-Type-Options: nosniff:** Leaves MIME-type sniffing vulnerabilities unmitigated.
  4. **Access-Control-Allow-Origin: `*`:** Wildcard configuration exposes response resources to any untrusted third-party domain.
* **Remediation:** Add custom response security headers in `next.config.js`:
  ```javascript
  // next.config.js
  const securityHeaders = [
    { key: 'X-Frame-Options', value: 'DENY' },
    { key: 'X-Content-Type-Options', value: 'nosniff' },
    { key: 'Referrer-Policy', value: 'strict-origin-when-cross-origin' },
    { key: 'Content-Security-Policy', value: "default-src 'self'; script-src 'self' 'unsafe-eval' 'unsafe-inline' https://www.googletagmanager.com; img-src 'self' data: https:;" }
  ];
  ```

---

### CYN-003 — Inconsistent Contact Details Between Site Footer & Contact Page
* **Severity:** **Medium** | **Priority:** **P2** | **Category:** Content / Usability | **Confidence:** Verified in Browser
* **Pages:** Site Footer (All Pages) vs `https://www.cynbit.in/contact`
* **Actual Result:**
  * **Footer:** Displays 1 email (`opportunities@cynbit.in`) and 3 phone numbers: `+91 89479 62667`, `+91 78912 09777`, `+91 83023 37367`.
  * **Contact Page:** Displays 2 emails (`opportunities@cynbit.in`, `support@cynbit.in`) and only 2 phone numbers. The Privacy Policy directs GDPR/data queries to `opportunities@cynbit.in` (an internship/hiring inbox).
* **Expected Result:** A centralized contact object across the entire application with designated routing for support, partnerships, and legal queries.
* **Remediation:** Centralize company contact definitions in a single configuration file (`constants/contact.ts`).

---

### CYN-008 & CYN-009 — Metadata Duplication & Shared Root Tags Across Subpages
* **Severity:** **Medium** | **Priority:** **P2** | **Category:** SEO | **Confidence:** Verified in Browser
* **Actual Result:**
  * Subpages (`/case-studies`, `/case-studies/*`, `/diaries`) fallback to the identical root homepage title: `"Cynbit Technologies | AI Automation & Software Solutions Jaipur"`.
  * Template concatenation generates duplicated brand strings: `"About Us | Cynbit Technologies | Cynbit Technologies"`.
  * `/diaries` contains an HTML double-escaped ampersand in the title (`&amp;amp;`).
* **Expected Result:** Dynamic Next.js Metadata API generating unique, concise `<title>` and `<meta name="description">` strings per route.

---

### CYN-010 & CYN-011 — Defective OpenGraph Architecture (`og:url` & SVG `og:image`)
* **Severity:** **Medium** | **Priority:** **P2** | **Category:** SEO / Social Sharing | **Confidence:** Verified in Browser
* **Actual Result:**
  * Subpages broadcast `og:url` as `https://cynbit.in/`, which strips subpage identity and points to the non-www apex domain.
  * `og:image` is set to `https://cynbit.in/logo.svg`. Major platforms (LinkedIn, X/Twitter, WhatsApp, Facebook) do not render vector SVG images in link cards.
* **Remediation:** Standardize on canonical `https://www.cynbit.in/${slug}` and output pre-rendered 1200x630px JPG/PNG social banners.

---

### CYN-017 — Accessible Name Pollution via Material Symbols Ligatures
* **Severity:** **Medium** | **Priority:** **P2** | **Category:** Accessibility (WCAG 2.1 AA) | **Confidence:** Verified in Browser
* **Actual Result:** Icon ligatures such as `"expand_more"`, `"arrow_forward"`, `"east"`, and `"send"` are embedded as raw inner text within clickable buttons. Screen readers announce: `"Join the newsletter east button"` or `"Company expand more link"`.
* **Remediation:** Wrap icon fonts with `<span aria-hidden="true" className="material-symbols-outlined">east</span>`.
