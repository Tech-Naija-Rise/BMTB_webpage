# Thought Book Website — Developer Documentation

Welcome. This folder explains the **website** in this repository: what it is for, how its page is organized, how the download button works, and how to maintain and test it.

## Start here

1. [Website overview](overview.md) — purpose, boundaries, and the request flow.
2. [Page structure](page-structure.md) — each section and what visitors use it for.
3. [Download flow](download-flow.md) — how the installer button finds a Windows release.
4. [Styles and assets](styles-and-assets.md) — layout, responsive behavior, and images.
5. [Maintenance and testing](maintenance-and-testing.md) — safe changes and a pre-release checklist.

## Important distinction

This repository contains a **static marketing/download website**. It is not the Thought Book desktop application, and it does not implement note storage, passwords, encryption, or auto-lock. Those features belong to the separate application repository:

- Website source: [Tech-Naija-Rise/BMTB_webpage](https://github.com/Tech-Naija-Rise/BMTB_webpage)
- Desktop application source: [Tech-Naija-Rise/thought_book](https://github.com/Tech-Naija-Rise/thought_book)
- Releases/downloads: [Tech-Naija-Rise/BMTB Releases](https://github.com/Tech-Naija-Rise/BMTB/releases)

## Documentation rule

These documents describe the website source currently in `index.html` and `README.md`. If the code changes, update the relevant document too. Hosting configuration and deployment automation are not defined by the page source alone; verify the repository settings and hosting provider before documenting or changing deployment steps.
