# Maintenance and testing

This guide is for a developer making a change to the Thought Book website. The current source is a static HTML page with inline CSS and JavaScript.

## Before changing anything

1. Read `index.html` and the relevant guide in this folder.
2. Identify whether the change affects page copy, styles, assets, the download behavior, or an external link.
3. Verify product-specific claims against the desktop app repository or current release notes.
4. Keep the change focused. This site does not currently require a JavaScript build step based on the checked-in source.

## Run a local preview

Because the site is static, a basic local preview is enough for most copy and layout work:

1. Open the repository folder on your computer.
2. Open `index.html` in a browser.
3. Refresh after saving changes.

For behavior involving the GitHub API, a local HTTP server is a more realistic preview than opening the file directly. If the browser blocks a request from a local file, test through a local server and inspect the browser Console and Network panels. Do not add a backend just to preview this page.

## Manual test checklist

### Content and navigation

- [ ] The page title and main headline are correct.
- [ ] Header links jump to Features, Privacy, and FAQ.
- [ ] Both calls to action link to the intended destinations.
- [ ] The desktop app source link opens the correct repository.
- [ ] The installation warning matches the current release limitations.
- [ ] No stale version number, dead link, or outdated product claim remains.

### Images and social preview

- [ ] Header logo loads.
- [ ] Main product screenshot loads and reflects the current app.
- [ ] Browser favicon loads.
- [ ] The Open Graph image path points to the intended social preview image.
- [ ] Images do not stretch or cause horizontal overflow.

### Download behavior

- [ ] Clicking the primary download button shows the temporary lookup state.
- [ ] When the latest release contains a `.exe` asset, the button requests that asset.
- [ ] When the API request fails or no `.exe` is present, the visitor is sent to the latest release page.
- [ ] The button label and busy state are restored after the lookup.
- [ ] The fallback release link remains usable if JavaScript is unavailable or the direct download does not start.

To test fallback behavior, use browser developer tools to simulate a failed request or test with a release that has no matching installer in a safe test environment. Do not change the real production release solely to test this case.

### Responsive and accessibility checks

- [ ] Test a wide desktop viewport, tablet-sized viewport, and narrow mobile viewport.
- [ ] Confirm no horizontal scrolling or clipped content.
- [ ] Navigate using the keyboard and check the visible focus indicator.
- [ ] Open and close FAQ items with the keyboard.
- [ ] Confirm download status text changes are visible to assistive technology.
- [ ] Enable reduced-motion preferences and confirm motion is minimized.

### Browser diagnostics

Open browser developer tools:

- **Console:** look for JavaScript errors and missing-resource messages.
- **Network:** check image requests and the GitHub Releases API request.
- **Elements/Inspector:** inspect responsive layout or unexpected spacing.

## Updating the product claims

The website describes local storage, offline-first behavior, password protection, encryption, auto-save, auto-lock, supported Windows version, and migration/password-recovery limitations.

Before changing any of these claims:

1. Check the current application source and release notes.
2. Distinguish what is implemented from what is planned.
3. Use plain language and avoid absolute security promises.
4. Update the matching FAQ, feature card, or installation warning.
5. Re-test the page and links.

## Deployment: what is known and what is not

The repository's `index.html` is static and can be served by a static web host. However, the HTML and README alone do **not** establish which host currently publishes the site, which branch/path it deploys from, whether a custom domain is configured, or whether a CI workflow handles deployment.

Before deploying:

1. Check the repository's **Settings → Pages** (if GitHub Pages is used).
2. Check the repository's Actions/workflows for any publishing workflow.
3. Confirm the actual hosting provider, published branch/folder, and domain with the maintainer.
4. Make sure `index.html` and the referenced `imgs/` files are included in the published source.
5. After publishing, open the public site and repeat the content, image, responsive, and download checks.

Do not add or change hosting configuration until the existing deployment method is confirmed.

## Suggested change workflow

- Create a dedicated branch for the website change.
- Make the smallest useful edit.
- Preview and test it locally.
- Review the diff to ensure only intended files changed.
- Open a pull request and describe how the change was tested.
- After merge/deployment, verify the live site.

This keeps content, styling, and download behavior maintainable without mixing website work into the separate desktop application.
