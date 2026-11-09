# Security: Page Attestation & AI Readiness Check for Confluence

Updated 9 November 2026

How the Atlassian Marketplace app **Page Attestation & AI Readiness Check for Confluence**, made by EvidencePair LLC, handles data, what protects it, how we handle vulnerabilities, and which certifications apply. What the app stores is listed in full in its [privacy policy](./PRIVACY_POLICY.md).

## Data handling

- **Forge only.** The app runs on Atlassian Forge (`nodejs24.x`) on Atlassian infrastructure. Its three screens (a page byline item, a space settings page and a global page) are built with Forge UI Kit.
- **No egress.** The manifest declares no external permissions and no remote services. The app makes requests only to your site's Confluence APIs, and it loads no analytics, error-reporting services or external assets.
- **No storage of its own.** The app keeps its data in Confluence on your site: a space property (`rovoGuardSpacePolicy`), a page property (`rovoGuardAttestation`) and two page labels (`verified-for-ai`, `stale-exclude-ai`). It uses no Forge storage or Forge SQL, and EvidencePair has no copy.
- **Requests run as the user.** Every request the app makes calls Confluence as the person using it, so Confluence applies that person's own permissions. The app never calls Confluence as itself. It has no scheduled jobs, triggers or other background functions, so it runs only when someone opens one of its screens.
- **Permissions it asks for.**
  - `read:page:confluence`: read the page a byline item is opened on, list up to 50 pages in a space, and read each page's `rovoGuardAttestation` property.
  - `write:page:confluence`: save a sign-off or quarantine record to its page.
  - `read:space:confluence`: read a space's `rovoGuardSpacePolicy` property.
  - `write:space:confluence`: save a space's policy.
  - `read:label:confluence`, `write:label:confluence`: add one of the app's two labels to a page and remove the other. The app never lists a page's labels.
  - `read:content-details:confluence`: declared in the manifest. The app does not read content details: apart from the page and space requests above, its only requests add and remove labels.
- **What the checksum is.** Each page record carries a SHA-256 checksum of its account ID, page ID, page version, time and decision. It does not cover the page's title, content or the note. It shows whether those five values still match what was written. It is not a digital signature: someone with permission to edit the page's properties could change the record and recompute the checksum. The checksum at the end of the CSV export works the same way, over the exporting account ID, the time and the rows.

## Encryption

The app stores nothing outside your Confluence site and sends nothing outside Atlassian's platform. Encryption in transit and at rest is provided by Atlassian as part of your site, as described in the [Atlassian Trust Center](https://www.atlassian.com/trust). The app adds no encryption of its own.

## Vulnerability management

- **Reporting.** Email security@evidencepair.com. Tell us the app, what you found and how to reproduce it. Please do not test against sites you do not own. We acknowledge every report within one business day.
- **Response.** EvidencePair adopted a written security incident response plan on 12 October 2026. It covers triage, containment, investigation, notification of Atlassian and affected customers, and recovery.
- **Dependencies.** The app's npm dependencies are pinned in its lockfile. Atlassian maintains and patches the Forge runtime.
- **Bug bounty.** We do not run a bug bounty programme.

## Certifications

EvidencePair holds no security certifications, and the app has had no independent penetration test or external audit. The infrastructure the app runs on is Atlassian's, and Atlassian's own certifications cover it: see the [Atlassian Trust Center](https://www.atlassian.com/trust).
