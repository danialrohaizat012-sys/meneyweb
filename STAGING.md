# Meney Web staging preview

This repository is static HTML. The staging site can be served with **GitHub Pages** for free, with no changes to meney.my.

## One-time setup (repository owner)
1. Open https://github.com/danialrohaizat012-sys/meneyweb/settings/pages
2. Under **Build and deployment**, select **Deploy from a branch**.
3. Select **main**, folder **/(root)**, then **Save**.
4. Wait for the Pages deployment to complete. Check https://github.com/danialrohaizat012-sys/meneyweb/actions
5. Open https://danialrohaizat012-sys.github.io/meneyweb/ for the public storefront.
6. For owner UAT only: https://danialrohaizat012-sys.github.io/meneyweb/catalogue-admin.html

## Firebase prerequisite
Firebase Console → Authentication → Settings → Authorized domains: add `danialrohaizat012-sys.github.io` if the owner sign-in flow reports an unauthorized-domain error. Email/password login often does not require this, but Google/popup auth does.

## UAT (use an existing safe product; avoid real stock changes)
- Open storefront in an incognito window. Unpublished products must not be shown.
- Login to Catalogue Publisher as an active Owner.
- Publish a safe test product. Refresh the storefront in incognito: only that published product should show.
- Unpublish it. Refresh: it must disappear.
- Test on desktop and mobile.
- Confirm POS and internal collections remain inaccessible to unauthenticated visitors.

## Safety
- GitHub Pages is a public website. Never commit passwords, Firebase service-account keys, customer data, or private inventory exports.
- Publisher access depends on Firestore Security Rules, not on the secrecy of its URL.
- Publishing is manual: edits to POS stock/price do not auto-sync to the public catalogue.
- No production DNS changes or live POS changes are needed for staging.
- A successful GitHub Actions static test does not constitute end-to-end UAT.
