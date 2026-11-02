# Cynbit Website — Comprehensive QA Audit & Testing Report

| | |
|---|---|
| **Target URL** | [https://www.cynbit.in/](https://www.cynbit.in/) |
| **Audit Date** | 2 November 2026 |
| **Testeing by** | Kartik Karnwal |
| **Audit Scope** | End-to-End Functional, Cross-Platform Responsive, Usability, Accessibility (WCAG 2.1 AA), SEO/Metadata, Security Headers & Privacy Compliance |
| **Execution Environment** | Interactive Browser Automation (Playwright/Chrome Headless/Headed), Mobile Emulation, Tablet Emulation, Desktop Viewports, Network/HTTP Diagnostics |
| **Report Status** | Final Comprehensive Deliverable |

---

## 1. Executive Summary

A comprehensive quality assurance (QA) audit was performed on **Cynbit Technologies** ([https://www.cynbit.in/](https://www.cynbit.in/)), a Jaipur-based software development and AI automation marketing and platform website built on Next.js and deployed via Vercel Edge infrastructure.

### Overall Quality 
* **System Availability & Core Navigation: — All 18 sampled routes render successfully; primary dropdowns and mobile navigation drawer operate cleanly without catastrophic crash.
* **Responsive Visual Adaptation:** **GOOD ** — Mobile (360px, 375px), Tablet (768px), and Desktop (1024px–1920px) adapt fluidly without severe horizontal page blowout.
* **Form Validation & Interactive States:** **POOR ** — Contact form fails silently on invalid inputs without inline error notifications; careers multi-step form enforces excessive personal data collection.
* **SEO, OpenGraph & Metadata:** **MODERATE ** — Severe tag duplication (`Brand | Cynbit Technologies | Cynbit Technologies`), universal fallback to homepage `og:url` (`https://cynbit.in`) on subpages, SVG preview image not widely supported on social cards.
* **Security & Infrastructure Headers:** **MODERATE ** — Valid `Strict-Transport-Security` (HSTS) with 2-year max-age, but missing `Content-Security-Policy` (CSP), `X-Frame-Options`, `X-Content-Type-Options: nosniff`, and wildcard `Access-Control-Allow-Origin: *`.

---

## 2. Test Environment Matrix & Execution Status

### 2.1 Executed Device & Viewport Matrix

All viewports were rigorously tested via live interactive browser agents:

| Device Category | Viewport Width x Height | Browsers / Engines Tested | Rendering Result | Evidence Artifact Reference |
|---|---|---|---|---|
| **Mobile Small** | 360 x 800 px | Chromium / Blink (Android Emulation) | **PASS** — Hamburger menu clean, single-column stack | `evidence/mobile_home_top_*.png`, `evidence/mobile_menu_open_*.png` |
| **Mobile Standard** | 375 x 667 px / 390 x 844 px | WebKit / Blink (iOS / iPhone layout) | **PASS** — Fluid cards, touch targets legible | `evidence/mobile_services_*.png`, `evidence/mobile_contact_*.png` |
| **Tablet Portrait** | 768 x 1024 px | Chromium (iPad / Android Tablet) | **PASS** — Persistent bottom dock nav + header menu | `evidence/tablet_homepage_*.png`, `evidence/tablet_homepage_scrolled_*.png` |
| **Laptop / Desktop** | 1024 x 768 px | Chromium Desktop | **PASS** — Grid structures intact | `evidence/cynbit_homepage_desktop_*.png` |
| **Desktop Full HD**| 1280 x 800 px / 1366 x 768 px | Chromium Desktop | **PASS** — Optimal display layout | `evidence/cynbit_homepage_viewport_*.png` |
| **Ultra-Wide Desktop**| 1920 x 1080 px | Chromium Desktop | **PASS** — Container max-widths prevent stretching | `evidence/cynbit_homepage_after_modal_close_*.png` |

---

## 3. Comprehensive Test Execution Matrix

| Test Suite ID | Test Case Title | Target URL / Flow | Methodology / Tool | Result | Key Findings / Bug Reference |
|---|---|---|---|:---:|---|
| **TC-NAV-01** | Global Navigation Desktop | All pages (`/`, `/story`, `/services`, etc.) | Interactive Browser | **PASS** | Dropdowns open smoothly; direct links resolve. |
| **TC-NAV-02** | Mobile Drawer & Bottom Dock | Mobile/Tablet Viewports | Interactive Browser | **PASS** | Mobile drawer slides out cleanly; bottom bar docked on tablet. |
| **TC-FORM-01** | Contact Form Empty Submit | `/contact` | Interactive Browser / DOM click | **FAIL** | Form fails silently without inline error or user notification. *(CYN-024 / CYN-026)* |
| **TC-FORM-02** | Contact Form Invalid Email | `/contact` | Form Input ("invalid-email") | **FAIL** | Native email formatting is bypassed or fails to display error popup. *(CYN-026)* |
| **TC-FORM-03** | Careers Form Data Collection | `/careers/qa-testing-intern` | DOM inspection & Form Flow | **FAIL** | Enforces excessive PII (DOB, Gender, WhatsApp, Permanent Address). *(CYN-004)* |
| **TC-BLOG-01** | Blog Pagination Navigation | `/blog`, `/blog?page=0`, `/blog?page=1` | Direct URL + Navigation | **FAIL** | No visible page 1/2 buttons; all posts continuous; query param does not filter. *(CYN-001)* |
| **TC-BLOG-02** | Blog Category Taxonomy | `/blog?category=IT Strategy` | Interactive Filter Buttons | **FAIL** | Filter buttons query parameter, but post tags differ from filter buttons. *(CYN-023)* |
| **TC-ERR-01** | Custom 404 Error State | `/this-page-does-not-exist` | Direct HTTP Navigation | **PASS** | Clean custom 404 UI ("Node Not Found") with working "Return to Base". |
| **TC-A11Y-01**| Keyboard Focus & Skip Link | `/` | Tab Sequence Navigation | **PARTIAL** | Tab navigation highlights elements, but lacks skip-to-content link. *(CYN-027)* |
| **TC-A11Y-02**| Material Symbols Text Leakage | Global Links / Buttons | DOM Content & Screen Reader | **FAIL** | Icon ligatures (`east`, `expand_more`, `arrow_forward`) leak into accessible name. *(CYN-017)* |
| **TC-A11Y-03**| Heading Semantics Hierarchy | `/bitelevate/paths` | DOM Tree Analysis | **FAIL** | Complete descriptive paragraph tagged as `<h2>`. *(CYN-018)* |
| **TC-SEO-01** | Route-Specific Title & Meta | `/case-studies`, `/diaries`, etc. | DOM `<head>` extraction | **FAIL** | Reuses root homepage title; double-encoded `&amp;` in title. *(CYN-008)* |
| **TC-SEO-02** | OpenGraph Host Uniformity | Global | Meta tags inspection | **FAIL** | Declares `og:url = https://cynbit.in` while domain canonical is `www.cynbit.in`. *(CYN-010)* |
| **TC-SEO-03** | OpenGraph Image Format | Global | Meta tags inspection | **FAIL** | Uses SVG logo instead of recommended 1200x630 raster PNG/JPG. *(CYN-011)* |
| **TC-SEC-01** | HTTPS & HTTP Redirection | `http://cynbit.in` -> `https://` | HTTP Head Requests | **PASS** | 308 Permanent Redirect to HTTPS, followed by 307 to `www.cynbit.in`. |
| **TC-SEC-02** | Security Headers (CSP / HSTS) | HTTP Response Analysis | PowerShell / cURL Head | **FAIL** | HSTS present; CSP, X-Frame-Options, X-Content-Type-Options missing. *(CYN-028)* |
| **TC-SEC-03** | Cookie Consent Compliance | Fresh browser session | Storage & DOM Analysis | **FAIL** | Google Analytics declared in Cookie Policy, but no consent banner triggered. *(CYN-005)* |
| **TC-CONT-01**| Consistency of Phone & Email | Footer vs `/contact` | Cross-page text check | **FAIL** | Footer lists 3 phones; `/contact` lists 2 phones; emails conflict. *(CYN-003)* |
| **TC-CONT-02**| Metric & Claim Consistency | `/case-studies`, `/`, `/team` | Cross-page text check | **FAIL** | Hero says 99.99% uptime, lower section says 99.9%; 100+ projects vs 13 studies. *(CYN-012)* |

---

## 4. Security & Infrastructure Audit Findings

### 4.1 HTTP Headers & Transport Security Analysis
Live execution against `https://www.cynbit.in/` revealed:
* **HSTS (`Strict-Transport-Security`):** `max-age=63072000` (2 years) — **PASSED**.
* **Content-Security-Policy (CSP):** **MISSING**. Without a CSP, the application is unprotected against cross-site scripting (XSS) and arbitrary resource injection.
* **X-Frame-Options / frame-ancestors:** **MISSING**. Allows the site to be framed in external iframes, presenting a clickjacking vulnerability.
* **X-Content-Type-Options:** **MISSING**. Does not prevent MIME-sniffing exploits.
* **Access-Control-Allow-Origin:** Configured as wildcard `*`, which exposes API endpoints unnecessarily to all origins.
* **Referrer-Policy:** Missing explicit declaration (should be `strict-origin-when-cross-origin`).

### 4.2 Redirect & Canonical Integrity
* `http://cynbit.in/` &rarr; `308 Permanent Redirect` &rarr; `https://cynbit.in/`
* `https://cynbit.in/` &rarr; `307 Temporary Redirect` &rarr; `https://www.cynbit.in/`
* **Defect:** Apex domain `https://cynbit.in/` issues a `307 Temporary Redirect` rather than a `301 Permanent Redirect`. Furthermore, `og:url` on all pages advertises `https://cynbit.in/`, creating canonical search indexing confusion.

---

## 5. Visual Evidence Artifacts Archive

All recorded visual and video evidence artifacts have been captured, structured, and archived in the project `evidence/` directory:

1. **Custom 404 Page:** `evidence/custom_404_page_1793616838130.png`
2. **Contact Form Silent Submit Failure:** `evidence/contact_form_validation_1793615961686.png`
3. **Contact Page Desktop Viewport:** `evidence/cynbit_contact_page_1793615518288.png`
4. **Blog Page Feed & Query Navigation:** `evidence/blog_page_query_1_1793616431627.png`
5. **Blog Article Typography & Metadata:** `evidence/blog_post_screenshot_1793616457773.png`
6. **Mobile (360px) Navigation Open:** `evidence/mobile_menu_open_1793615665973.png`
7. **Mobile (360px) Services Stack:** `evidence/mobile_services_1793615741604.png`
8. **Tablet (768px) Responsive Viewport:** `evidence/tablet_homepage_1793615835505.png`
9. **Desktop Full Layout:** `evidence/cynbit_homepage_desktop_1793615340730.png`
10. **Interactive Video Session Recordings:** `evidence/blog_pagination_test_1793616311000.webp` and `evidence/mobile_responsive_test_1793615629447.webp`
