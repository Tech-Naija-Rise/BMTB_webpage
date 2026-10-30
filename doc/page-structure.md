# Page structure

This guide follows the order a visitor encounters sections in `index.html`.

## 1. Document head

The `<head>` sets the browser title, viewport behavior, theme color, search description, social-sharing metadata, and favicon. It also contains the page's CSS.

Key items:

- `<title>`: browser-tab title.
- `meta name="description"`: short description used by search engines and some previews.
- `og:title`, `og:description`, `og:image`: Open Graph information used by social platforms when they generate a link preview.
- `link rel="icon"`: browser tab icon.
- `<style>`: all current site styling.

The Open Graph image path is `imgs/BMTB_demo.png`; confirm the file exists and looks right whenever the social preview is changed.

## 2. Header and navigation

The header shows the Thought Book logo/name and links to the page's Features, Privacy, and FAQ sections, plus the desktop app's GitHub repository.

The section links use HTML fragment IDs:

- `#features`
- `#privacy`
- `#faq`

If a section ID changes, update its navigation link too.

## 3. Hero section

The hero is the first main section. It includes:

- A short Windows 11/product label.
- The main headline and product explanation.
- The primary **Download for Windows** button.
- A secondary link to the desktop app source.
- A status line that explains the download context.
- A three-part privacy facts strip covering local storage, app-level password/encryption protection, and the absence of a hosted notes account.
- A framed official-release download area.
- A screenshot of the desktop application.

This is the most important section for first-time visitors. Keep its message understandable and make sure the screenshot matches the current app.

## 4. Features

The `#features` section contains six feature cards describing the product: local storage, password protection, encryption, automatic saving, auto-lock, and a focused desktop experience.

These cards are explanatory text, not controls. They do not call app functionality from the website. Keep each claim consistent with the actual desktop app.

## 5. Privacy section

The `#privacy` section reinforces the local-storage and offline-first positioning. It includes a link to review the desktop app source and a short list of privacy-related product points.

Do not imply that the website is the storage location for notes; the notes belong to the desktop application.

## 6. Installation warning

A highlighted notice warns visitors about important release limitations, including Windows 11 targeting, lack of migration from older versions, possible database overwrite, and lack of password recovery.

Treat this warning as important user-facing information. Before editing it, check the current app release notes so the website does not accidentally hide or misstate a data-loss risk.

## 7. FAQ

The FAQ uses native HTML `<details>` and `<summary>` elements. Visitors can open a question to reveal its answer; no JavaScript is needed for that interaction.

Questions cover offline use, note storage, password recovery, older-version compatibility, and source-code access.

## 8. Closing call to action

Near the bottom, the closing panel repeats the download action and source-code link. It gives visitors another chance to act after reading the page.

## 9. Footer

The footer includes the current year and links to the source repository and latest releases. The year is filled in by JavaScript at page load.

## Page map

```text
index.html
|
+-- head
|   +-- metadata / social preview / favicon
|   +-- CSS
|
+-- body
    +-- header: logo + navigation
    +-- main
    |   +-- hero: message + download + screenshot
    |   +-- features: six cards
    |   +-- privacy: privacy message + checklist
    |   +-- install warning
    |   +-- FAQ: expandable questions
    |   +-- closing call to action
    +-- footer: year + links
    +-- script: year + download-button behavior
```

## Editing guidance

Prefer small, focused changes. Keep links, section IDs, visible copy, accessibility attributes, and mobile behavior in sync. After moving or renaming a section, test every navigation link and both download call-to-action areas.
