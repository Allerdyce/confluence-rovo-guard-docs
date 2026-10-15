# Privacy Policy, Data Residency & Security Statement — Page Attestation & Rovo AI Readiness Guard for Confluence

**Effective Date**: October 14, 2026  
**Publisher**: EvidencePair LLC  
**App Key**: `com.evidencepair.confluence.rovo.guard`  
**App ID**: `ari:cloud:ecosystem::app/8bae494e-64cf-44ba-bfc1-843b7b6eb133`

---

## 1. Zero Data Egress & Architecture Statement ("Runs on Atlassian")

**Page Attestation & Rovo AI Readiness Guard for Confluence** executes 100% inside Atlassian's managed Forge Cloud runtime (`nodejs24.x`) and declares **zero external remote endpoints (`remotes:`)** and **zero external egress permissions**.

- **0 Bytes External Storage**: EvidencePair LLC does not operate any external servers, databases, or telemetry endpoints that receive customer data from Page Attestation & Rovo AI Readiness Guard for Confluence.
- **100% Native Confluence Space & Content Property Storage (<32 KB Enforced)**:
  - Space-level Rovo AI readiness policies are stored exclusively inside your Confluence instance's **Space Properties** (`/wiki/api/v2/spaces/{spaceId}/properties`, key `rovoGuardSpacePolicy`).
  - Page-level SHA-256 cryptographic attestations and quarantine records are stored exclusively inside your Confluence instance's **Page Content Properties** (`/wiki/api/v2/pages/{pageId}/properties`, key `rovoGuardAttestation`).
  - Page labels (`verified-for-ai` and `stale-exclude-ai`) are stored exclusively as native Confluence content labels (`/wiki/rest/api/content/{pageId}/label`).
  - Zero Forge SQL and Zero Forge KVS storage are used.

---

## 2. Data Residency & Compliance Inheritance

Because Page Attestation & Rovo AI Readiness Guard for Confluence stores 100% of its policy configurations and page attestation signatures within native Confluence Space and Page Properties:
- **Automatic Data Residency**: All app data automatically resides in the exact geographic region (US, EU, AU, DE, SG, CA, UK, JP, etc.) configured for your host Confluence Cloud product under Atlassian Data Residency.
- **Lifecycle & Deletion**: All app properties are automatically included in standard Confluence Cloud backups and are permanently deleted when the host page, space, or property is deleted by your administrator.

---

## 3. Privacy Policy (GDPR / CCPA / SOC 2 / ISO 42001 Alignment)

### Personal Data Processed
To provide cryptographic attribution on page sign-off and quarantine events, the app records:
- **Atlassian Account ID (`accountId`)** of the user signing off or quarantining a Confluence page.
- **ISO-8601 UTC Timestamp (`timestamp`)**, page version number (`attestedPageVersion`), and attestation decision (`VERIFIED_FOR_AI` or `STALE_EXCLUDE_AI`).
- **Stores Personal Data Declaration**: No external PII (such as names, emails, or phone numbers) is stored or exported outside the Atlassian Cloud host tenant.

### How Data Is Used
- Processed solely within the Atlassian Forge runtime to compute and verify a deterministic SHA-256 integrity signature (`accountId|pageId|pageVersion|timestamp|decision`).
- Never transmitted outside your Atlassian Cloud tenant, never sold, and never shared with third parties.

### Data Subject Rights (Access, Rectification, Erasure)
Space and organization administrators have full read/write/delete control over all app properties via standard Confluence REST API v2 endpoints:
- `GET` / `PUT` / `DELETE /wiki/api/v2/spaces/{spaceId}/properties/{propertyId}` (`rovoGuardSpacePolicy`)
- `GET` / `PUT` / `DELETE /wiki/api/v2/pages/{pageId}/properties/{propertyId}` (`rovoGuardAttestation`)

---

## 4. Security Contact
Security inquiries or vulnerability reports may be submitted to **EvidencePair LLC** at `support@titlecovenant.com`.
