# Cynbit Website — Complete QA Audit Deliverables Package

This repository contains the full Quality Assurance (QA) audit report, comprehensive bug database, prioritized remediation recommendations, and multi-device visual evidence for the **Cynbit Technologies** website ([https://www.cynbit.in/](https://www.cynbit.in/)).

---

## 📂 Deliverables Structure

* **[01-qa-audit-report.md](file:///c:/Users/Kartik/Desktop/TEST/01-qa-audit-report.md)**: Full QA Audit Report covering testing methodology, executed device & viewport matrix (mobile 360px/375px, tablet 768px, desktop 1024px–1920px), test execution matrix, HTTP security headers analysis, canonical redirect verification, and accessibility evaluation.
* **[02-bug-issue-report.md](file:///c:/Users/Kartik/Desktop/TEST/02-bug-issue-report.md)**: Master Bug & Issue Report detailing 28 logged defects categorized by Severity (High, Medium, Low), Priority (P1, P2, P3), with exact steps to reproduce, actual vs expected results, affected URLs, and code remediation snippets.
* **[03-improvement-recommendations.md](file:///c:/Users/Kartik/Desktop/TEST/03-improvement-recommendations.md)**: Prioritized engineering roadmap for developer fixes (Tier 1 P1 hotfixes, Tier 2 P2 architecture improvements, Tier 3 P3 technical debt), CI/CD automation strategy (Playwright E2E, axe-core a11y, Lighthouse CI), and phased delivery schedule.
* **`evidence/`**: High-resolution screenshots and session video captures documenting all responsive viewports, form validation behavior, 404 page states, and navigation interactions.

---

## 🔍 Key Findings Snapshot

1. **Contact Form Silent Failure (P1 / High):** Submitting empty or invalid email inputs fails without inline feedback or field alerts (`CYN-026`).
2. **Excessive PII on Careers Workflow (P1 / High):** Mandatory requirements for Date of Birth, Gender, WhatsApp, and Permanent Address for entry-level applicants contradict privacy declarations (`CYN-004`).
3. **Missing Cookie Consent Banner (P1 / High):** Third-party Google Analytics cookies declared in policy without opt-in consent controls (`CYN-005`).
4. **Missing Security Headers (P2 / Medium):** Site lacks CSP, X-Frame-Options (clickjacking vulnerability), and X-Content-Type-Options (`CYN-028`).
5. **SEO & Metadata Dilution (P2 / Medium):** Subpages inherit root homepage titles; duplicate brand names in title tag template; `og:url` universally set to apex non-www host (`CYN-008`, `CYN-009`, `CYN-010`).
6. **Inconsistent Company Data (P2 / Medium):** Discrepancies between footer and contact page phone numbers/emails; conflicting uptime statistics (99.99% vs 99.9%) (`CYN-003`, `CYN-012`).

---

**Prepared by:** Kartik Karnwal  
**Role:** QA Testing Intern Candidate  
**Date:** 2 November 2026
