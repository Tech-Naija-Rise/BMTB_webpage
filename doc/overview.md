# Website overview

## What this website does

The Thought Book website introduces the Thought Book Windows desktop notes app and helps visitors decide whether to try it. It explains the product's stated benefits, shows a product screenshot, answers common questions, links to the application source, and directs people to the latest Windows release.

It is a **static website** built from one main HTML file. The page's markup, styling, and small amount of browser-side JavaScript are all in `index.html`. The source shown in this repository does not use a frontend framework, package manager, or build step.

## What it does not do

The website itself does not:

- Create, read, or store a visitor's notes.
- Register users or manage accounts.
- Verify passwords or encrypt notes.
- Implement the desktop app's auto-save or auto-lock behavior.
- Host the Windows installer inside this repository.
- Provide a website backend or database.

Those responsibilities belong to the desktop app or the GitHub release service, not this page.

## Main pieces

| Piece | File / location | Responsibility |
|---|---|---|
| Page content and structure | `index.html` | Headings, navigation, feature cards, FAQ, links, footer |
| Visual design | `<style>` inside `index.html` | Colors, typography, spacing, cards, responsive layout |
| Browser behavior | `<script>` inside `index.html` | Current year and installer lookup |
| Images and icon | `imgs/` | Logo, screenshot, and social-preview image |
| Project information | `README.md` | Repository introduction and important installation warnings |
| Developer documentation | `doc/` | Guides for understanding and maintaining the website |

## Visitor journey

```text
Visitor opens website
        |
        v
Reads product message and sees screenshot
        |
        +------> Opens Features / Privacy / FAQ sections
        |
        +------> Opens desktop app source on GitHub
        |
        v
Clicks "Download for Windows"
        |
        v
Website asks GitHub for the latest release metadata
        |
        +------> Finds a .exe asset -> requests that download
        |
        +------> Lookup fails / no .exe -> opens release page
```

The page can be read without an account. Visiting the website does not itself create a Thought Book account. An internet connection is needed to fetch the installer from GitHub.

## External services and destinations

The source contains links to three main destinations:

- **Latest release page:** `https://github.com/Tech-Naija-Rise/BMTB/releases/latest`
- **GitHub Releases API:** `https://api.github.com/repos/Tech-Naija-Rise/BMTB/releases/latest`
- **Desktop app source:** `https://github.com/Tech-Naija-Rise/thought_book`

The download button uses the API to find an asset ending in `.exe`. The other release links take visitors to GitHub's latest-release page.

## Privacy and accuracy notes

The marketing page makes product claims about local storage, password protection, and encryption. Those are claims about the desktop application; the website does not implement them. If app behavior changes, verify the application repository and release notes before changing these statements.

The download interaction contacts GitHub's public API when the visitor clicks the button. Do not describe the website as making no network requests at all. The HTML source does not show a custom website backend or analytics integration.

## Where to make changes

- Change page wording or page sections in `index.html`.
- Change colors, responsive rules, and component appearance in its `<style>` block.
- Change installer lookup behavior in its `<script>` block.
- Change images in `imgs/` and update their references in the HTML.
- Change general repository introduction in `README.md`.
