# Privacy policy: Page Attestation & AI Readiness Check for Confluence

Updated 10 November 2026

This policy describes the Atlassian Marketplace app **Page Attestation & AI Readiness Check for Confluence** ("the app"), made by EvidencePair LLC ("EvidencePair", "we"). EvidencePair's company privacy policy, which covers our website and email you send us, is at <https://evidencepair.com/privacy/>.

## In short

- The app runs on Atlassian Forge, inside your Confluence site. It declares no external egress and no remote services, and it makes requests only to your site's Confluence APIs.
- It keeps its data in Confluence itself, as a space property, a page property and two page labels. That data is never sent to EvidencePair.
- The only personal data it stores itself is the Atlassian account ID of the person who signs off or quarantines a page, and of the person who last saved a space's policy. It also copies each signed page's title into that page's record.

## What the app stores

**One space property, `rovoGuardSpacePolicy`, per space whose policy someone has saved:**

- the space's ID and key, read from Confluence when the policy is saved. Earlier versions of the app wrote a fixed value (`MFS`) into the key field instead of your space's key. Saving the policy again replaces it;
- the policy: the attestation expiry window in days (30, 60 or 90 on the settings screen), and whether editing a page after sign-off makes the sign-off stale;
- the two label names the app uses, `verified-for-ai` and `stale-exclude-ai`;
- the Atlassian account ID of the person who last saved the policy, and when;
- the size of the record in bytes, and a schema version number.

**One page property, `rovoGuardAttestation`, per page that someone has signed off or quarantined:**

- the page's ID, its space's ID, and the page's title at the time;
- the decision: `VERIFIED_FOR_AI` (signed off) or `STALE_EXCLUDE_AI` (quarantined);
- the Atlassian account ID of the person who made the decision, and when;
- the page's version number at the time;
- a short note. The app's screens write one of three fixed sentences here. They have no field for typing a note;
- a SHA-256 checksum of the account ID, page ID, page version, time and decision. It lets the app tell whether those values have changed since they were written. The checksum adds no information of its own;
- the size of the record in bytes, and a schema version number.

Each new decision replaces the page's previous record, so the property holds only the latest one. Bulk quarantine on the app's global page writes a new record to every page it quarantines, under the account ID of the person who ran it.

**Two page labels.** Signing off a page adds the label `verified-for-ai` and removes `stale-exclude-ai`. Quarantining a page does the opposite. These are ordinary Confluence labels.

The app does not look up names, email addresses or profiles. A page title can contain personal data, and the app copies it as it is.

The global page also builds a CSV export each time it scans a space. For each page it scanned, the CSV lists the page's ID, title, current and signed versions, status, label, whether the checksum matched, the signer's account ID, the time and the checksum. Its last line holds the account ID of the person viewing it, the time, and a checksum of the rows. The app shows the CSV on screen to copy and does not save it anywhere.

## What the app reads from Confluence

- On a page's byline: the page's ID, title, version number and space ID; its `rovoGuardAttestation` property; and the `rovoGuardSpacePolicy` property of its space. The page is the one Confluence names in the byline's context.
- On a space's settings screen: that space's ID, key and name, and its `rovoGuardSpacePolicy` property. The space is the one Confluence names in the screen's context.
- On the global page: first, the ID, key and name of the spaces you can see (up to 500), so you can choose one. It reads nothing else until you choose. Then, for the space you chose: its ID, key and name; its policy; the first 50 pages Confluence returns, using each page's ID, title and version number; and each of those pages' `rovoGuardAttestation` property.
- When someone signs off or quarantines a page, the app reads the policy of that page's own space. When that space has no saved policy, the app uses its default policy (90 days, version-drift check on).

The app has no built-in space, page or account IDs. When Confluence names no page or space and you have chosen none, the app shows a message and reads and writes nothing.

It does not ask Confluence for page content, comments, attachments or a page's existing labels.

## Where the data lives

Space properties, page properties and labels are part of your Confluence site's data. Atlassian stores them with the rest of your site, in your site's data residency location, under Atlassian's own security and privacy commitments. The app has no storage of its own: it uses no Forge storage and no Forge SQL, and EvidencePair runs no servers in its path.

## Who can see it

The app makes every request as the person using it, so Confluence applies that person's own permissions. Confluence shows a page property to anyone who can view the page, through Confluence's REST API. The app's byline item shows the signer's account ID, the time and the checksum to anyone who opens it on the page. Anyone who can see a page can therefore see who last signed it off or quarantined it. The global page's CSV shows the same details for every page it scans that the viewer can see. The labels show on the page like any other label.

Confluence's permissions also decide who can change the data. Changing a page's property needs permission to edit the page. Confluence's space permissions decide who can read and change a space's policy.

## Retention and deletion

The app keeps both properties and the labels until someone deletes or replaces them. It has no retention setting, deletes nothing on its own schedule, and has no uninstall step. When a sign-off goes stale or expires, only the status the app shows changes. The record stays. When Confluence permanently deletes a page or a space, the properties attached to it go too. A Confluence administrator can delete either property at any time through Confluence's REST API, and remove the labels like any other label. They should do so before uninstalling if the data must go.

## Account closure

The app does not take part in Atlassian's personal data reporting. When an Atlassian account is closed, its account ID stays in the record of every page that person last signed off or quarantined, and in any space policy they last saved, until that property, the page or the space is deleted. The checksum covers the account ID, so if the ID is edited out of a page's record, the app shows that page as `TAMPER_DETECTED`. Deleting the property returns the page to `PENDING_ATTESTATION`.

## Platform logs

The app writes nothing to the Forge platform's logs. Atlassian's platform can still record errors it sees while the app runs, such as an unhandled error and its message ([Atlassian: view app logs](https://developer.atlassian.com/platform/forge/view-app-logs/)).

## Email and support

If you email us, our [company privacy policy](https://evidencepair.com/privacy/) describes how we handle that email, and the current restrictions on where our apps may be used.

## What we never do

We do not sell personal data or use it for unrelated advertising or AI training. The app's data stays in your Confluence site and never reaches us.

## Changes to this policy

The date at the top changes when this policy does. Every version is kept in this repository's history.

## Contact

hello@evidencepair.com
