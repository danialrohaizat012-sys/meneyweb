# Meney Web · Phase 1

Public storefront for Meney Gaming. Planned production domain: **https://meney.my**.

## Status
- Initial public homepage and responsive catalogue shipped as source code.
- **Not deployed**. Domain/DNS not changed. Firestore rules not changed.
- Catalogue starts empty by design. No internal POS product is exposed.
- WhatsApp checkout only. No payment gateway or inventory write from browser.

## Files
- `index.html`: storefront, product catalogue, trade-in, repair, WhatsApp.
- `firestore-public-catalogue.rules.snippet`: **additive snippet only**; not a complete rules file.

## Publishing contract
The public site reads `publicCatalogue` from Firebase project `meney-daily-mission`.
Each document must have `published: true` to appear. Default **false** when creating
a listing. Website also hides `available: false`.

Example **public-only** document:
```json
{
  "name": "PlayStation 5 Slim",
  "category": "Console",
  "brand": "Sony",
  "condition": "New",
  "price": 2199,
  "imageUrl": "https://example.com/ps5.jpg",
  "available": true,
  "published": false,
  "sourceProductId": "INTERNAL-PRODUCT-ID"
}
```
Do NOT copy `cost`, `supplier`, `profit`, `margin`, `customer`, `notes`,
or any other internal fields to publicCatalogue.

**Important:** A direct client-side sync from POS cannot safely create public documents
without trusted server code. Phase 2 should add an owner-only publishing workflow,
a trusted Cloud Function or validated backend sync, and inventory tests. Do not
give all staff publicCatalogue write access.

## Firestore rules deployment
1. Back up currently deployed rules.
2. Merge the snippet inside the existing `match /databases/{database}/documents` block.
3. Test anonymous `get/list` of published and unpublished documents,
   owner create/update/delete, and denial of public writes.
4. Test all existing POS/Accounting/KroniMeney/Staff workflows.
5. Deploy only after approval and successful tests.

## Domain & hosting
The repository is static and can be previewed on GitHub Pages or hosted on
Firebase Hosting. Domain **meney.my** is owned via Hostinger.
Do not alter DNS before selecting hosting, validating TLS, and confirming rollback.

For eventual `/pos`, `/accounting`, `/command`, `/mission`, `/kroni`,
and `/quest` routes, first verify production file versions and service-worker
scope. Do not copy legacy root-scoped PWAs unchanged under a shared origin.

## Acceptance tests
- Public homepage works on phone and desktop.
- Empty/unavailable catalogue displays a helpful message.
- Anonymous users can read only explicitly published catalogue records.
- Unpublished records never appear.
- Product search and category filters work.
- WhatsApp links use 601175956474.
- Existing POS/Accounting operations unaffected.
