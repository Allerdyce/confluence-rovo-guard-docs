# Privacy, Data Residency & Security Statement — Page Attestation & AI Readiness Check for Confluence

> The app's privacy policy is [PRIVACY_POLICY.md](./PRIVACY_POLICY.md), and its security documentation (data handling, encryption, vulnerability management and certifications) is [SECURITY.md](./SECURITY.md). This page is the architecture summary.

**Effective Date**: October 14, 2026  
**Publisher**: EvidencePair LLC  
**App Key**: `com.evidencepair.confluence.rovo.guard`  
**App ID**: `ari:cloud:ecosystem::app/8bae494e-64cf-44ba-bfc1-843b7b6eb133`  
**Security Contact**: `security@evidencepair.com`  
**Support**: <https://evidencepair.com/support/> (`support@evidencepair.com`)

---

## 1. Zero Data Egress & Architecture Statement ("Runs on Atlassian")

**Page Attestation & AI Readiness Check for Confluence** executes 100% inside Atlassian's managed Forge Cloud runtime (`nodejs24.x`) and declares **zero external remote endpoints (`remotes:`)** and **zero external egress permissions**.

- **0 Bytes External Storage**: EvidencePair LLC does not operate any external servers, databases, or telemetry endpoints that receive customer data from Page Attestation & AI Readiness Check for Confluence.
- **100% Native Confluence Space & Content Property Storage (<32 KB Enforced)**:
  - Space-level Rovo AI readiness policies are stored exclusively inside your Confluence instance's **Space Properties** (`/wiki/api/v2/spaces/{spaceId}/properties`, key `rovoGuardSpacePolicy`).
  - Page-level SHA-256 attestations and quarantine records are stored exclusively inside your Confluence instance's **Page Content Properties** (`/wiki/api/v2/pages/{pageId}/properties`, key `rovoGuardAttestation`).
  - Page labels (`verified-for-ai` and `stale-exclude-ai`) are stored exclusively as native Confluence content labels (`/wiki/rest/api/content/{pageId}/label`).
  - Zero Forge SQL and Zero Forge KVS storage are used.

---

## 2. Data Residency & Deletion

Because Page Attestation & AI Readiness Check for Confluence stores 100% of its policy configurations and page attestation records within native Confluence Space and Page Properties:
- **Automatic Data Residency**: All app data automatically resides in the exact geographic region (US, EU, AU, DE, SG, CA, UK, JP, etc.) configured for your host Confluence Cloud product under Atlassian Data Residency.
- **Lifecycle & Deletion**: App properties and labels stay until someone deletes them. Properties go when Confluence permanently deletes the page or space they belong to, or when your administrator deletes the property. Uninstalling the app deletes nothing.

---

## 3. Personal Data

The full privacy policy is [PRIVACY_POLICY.md](./PRIVACY_POLICY.md).

### Personal Data Processed
To attribute page sign-off and quarantine events, the app records:
- **Atlassian Account ID (`accountId`)** of the user signing off or quarantining a Confluence page, in that page's `rovoGuardAttestation` property.
- **ISO-8601 UTC Timestamp (`timestamp`)**, page version number (`attestedPageVersion`), page title at the time (`pageTitle`), and attestation decision (`VERIFIED_FOR_AI` or `STALE_EXCLUDE_AI`).
- **Atlassian Account ID (`updatedBy`)** of the user who last saved a space's policy, in that space's `rovoGuardSpacePolicy` property.
- **No names, emails or phone numbers**: The app stores none of these, and stores or exports nothing outside your Atlassian Cloud site.

### How Data Is Used
- Processed solely within the Atlassian Forge runtime to compute and verify a SHA-256 checksum (stored as `signature`) of `accountId|pageId|pageVersion|timestamp|decision`.
- Never transmitted outside your Atlassian Cloud site, never sold, and never shared with third parties.

### Access, Correction & Deletion
Space and organization administrators have read/write/delete control over all app properties via standard Confluence REST API v2 endpoints:
- `GET` / `PUT` / `DELETE /wiki/api/v2/spaces/{spaceId}/properties/{propertyId}` (`rovoGuardSpacePolicy`)
- `GET` / `PUT` / `DELETE /wiki/api/v2/pages/{pageId}/properties/{propertyId}` (`rovoGuardAttestation`)

The app does not take part in Atlassian's personal data reporting. A closed account's ID stays in these properties until they, the page or the space are deleted.

---

## 4. Security Contact
To report a security issue, email `security@evidencepair.com`. We acknowledge every report within one business day. EvidencePair holds no security certifications; see [SECURITY.md](./SECURITY.md). For support, use <https://evidencepair.com/support/> (`support@evidencepair.com`).
