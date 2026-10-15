# Atlassian Marketplace Partner Listing Copy — Page Attestation & Rovo AI Readiness Guard for Confluence

## App Identity
- **App Name**: Page Attestation & Rovo AI Readiness Guard for Confluence
- **App Key**: `com.evidencepair.confluence.rovo.guard`
- **App ID**: `ari:cloud:ecosystem::app/8bae494e-64cf-44ba-bfc1-843b7b6eb133`
- **Vendor**: EvidencePair LLC
- **Category**: Document Management / Governance & Compliance / AI Readiness
- **Runs on Atlassian Badge Eligibility**: **100% Eligible** (Native Forge `nodejs24.x`, Zero Remotes, Zero Forge SQL/KVS, Zero Data Egress)

---

## Tagline / Summary
> Cryptographic SHA-256 page attestation, version-drift guard & Rovo AI hygiene radar.

---

## Full Marketplace Description

### Stop Stale Runbooks & Unverified Drafts from Polluting Rovo AI Responses

When enterprise teams enable **Atlassian Rovo AI** across Confluence Cloud, AI answers are only as trustworthy as the underlying pages. Legacy on-premise runbooks, expired policies, and pages edited after compliance review (`currentPageVersion > attestedPageVersion`) can cause AI assistants to surface outdated operational instructions.

**Page Attestation & Rovo AI Readiness Guard for Confluence** gives Confluence administrators and page owners cryptographic SHA-256 sign-off, automatic version-drift invalidation, Rovo AI label governance (`verified-for-ai` / `stale-exclude-ai`), and a global content hygiene radar—built 100% on Atlassian Forge (`nodejs24.x`) with **zero external servers** and **zero data egress**:

1. **Cryptographic Page Sign-Off Byline Modal (`confluence:contentBylineItem`)**:
   - Page owners verify or quarantine pages in 1 click directly from the Confluence page byline.
   - Computes a deterministic **Web Crypto SHA-256 signature** (`accountId|pageId|pageVersion|timestamp|decision`) stored in Confluence Content Property `rovoGuardAttestation` (`<32 KB`) and syncs `verified-for-ai` or `stale-exclude-ai` page labels.
2. **Space Attestation Policy Engine (`confluence:spaceSettings`)**:
   - Configure space-wide attestation expiry windows (`30`, `60`, or `90` days), automatic version-drift invalidation (`currentPageVersion > attestedPageVersion`), and Rovo AI inclusion/exclusion labels in Space Property `rovoGuardSpacePolicy` (`<32 KB`).
3. **Global Rovo Content Hygiene Radar, Bulk Quarantine & Signed CSV Export (`confluence:globalPage`)**:
   - Scan all pages in a space, quarantine drifted or expired runbooks in 1 click (`stale-exclude-ai`) with SHA-256 audit logging, and export a cryptographically signed RFC-4180 CSV compliance report.

---

## Version Highlights (Highlights 1–3)

### Highlight 1: Cryptographic SHA-256 Page Byline Attestation & Label Sync
Empower page owners to sign off SOPs as `VERIFIED_FOR_AI` or quarantine legacy pages as `STALE_EXCLUDE_AI` directly from the Confluence byline. Every decision records a tamper-evident SHA-256 digest (`accountId|pageId|pageVersion|timestamp|decision`) in Confluence v2 Content Properties (`<32 KB`) and syncs `verified-for-ai` or `stale-exclude-ai` labels.

### Highlight 2: Space Rovo AI Readiness & Version-Drift Policy Engine
Configure 30, 60, or 90-day attestation expiry windows and automatic version-drift invalidation in Space Settings (`rovoGuardSpacePolicy`). Whenever an attested page is edited (`currentPageVersion > attestedPageVersion`), it is automatically flagged for re-attestation so unreviewed edits never slip through.

### Highlight 3: Global Rovo Content Hygiene Radar, 1-Click Bulk Quarantine & CSV Export
Audit every page across your Confluence space from a single Onest-styled radar dashboard. Execute 1-Click Bulk Quarantine (`stale-exclude-ai`) on drifted or expired runbooks with SHA-256 audit logging, and export a signed RFC-4180 compliance CSV report for SOC 2 and ISO 42001 AI governance audits.
