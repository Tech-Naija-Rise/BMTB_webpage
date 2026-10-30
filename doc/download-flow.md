# Download button: how it works

The primary download button is wired by the JavaScript near the bottom of `index.html`. It does not serve an installer from this website repository. Instead, it asks GitHub for the latest release of the desktop application.

## Flow in simple terms

```text
Visitor clicks either download button
          |
          v
Native confirmation dialog explains database overwrite
and password-recovery risks
          |
          v
Visitor types DOWNLOAD to continue
          |
          v
Visitor submits confirmation
          |
          v
Prevent normal link navigation
and show "Finding the latest installer…"
          |
          v
GET api.github.com/repos/Tech-Naija-Rise/BMTB/releases/latest
          |
          v
Did GitHub return a successful response?
      /                       \
    yes                       no
     |                         |
     v                         v
Read release JSON          Open latest release page
     |
     v
Find first asset whose name ends in .exe
and has a browser_download_url
     |
     +------ no matching asset ------> Open latest release page
     |
     v
Create temporary link to the asset
and trigger a browser download
     |
     v
Show a short success/status message
and restore the button label
```

## Important identifiers

The script defines the latest release page URL:

```js
const latestReleaseUrl =
  "https://github.com/Tech-Naija-Rise/BMTB/releases/latest";
```

It requests release metadata from:

```text
https://api.github.com/repos/Tech-Naija-Rise/BMTB/releases/latest
```

The script searches the returned `assets` list for an asset name matching `/\.exe$/i`. This means the filename must end in `.exe`, without regard to letter case. It then uses that asset's `browser_download_url`.

## What visitors see

1. Clicking either download button opens a confirmation dialog. It explains the risk to older notes and the lack of password recovery. The visitor must type `DOWNLOAD` to proceed; cancelling or pressing Escape stops the flow.
2. After confirmation, the buttons temporarily change to **Finding the latest installer…** and the status text says that GitHub is being checked.
3. If an installer is found, the script creates a temporary link, clicks it programmatically, removes it, and changes the button text briefly.
4. If the request fails or no matching installer exists, the browser is sent to the latest GitHub release page so the visitor can inspect available downloads manually.
5. After about 2.5 seconds, the script restores the original button label and clears its busy state.

The browser may handle the download in a way that varies by browser settings. The page's status message appropriately tells visitors to open the release page if the download did not start.

## Why use the latest release endpoint?

The page does not need a hard-coded version number or installer filename. As long as the latest GitHub release contains a Windows `.exe` asset, the button can discover that asset at click time.

## Common failure cases

| Symptom | Possible reason | What to check |
|---|---|---|
| Release page opens instead of a direct download | API request failed, no `.exe` asset was found, or the response was not successful | Open the latest release page and inspect its assets |
| API returns no usable release | No published latest release is available, or the repository/release is inaccessible | Check the release URL and release visibility |
| Release exists but button falls back | Asset filename does not end in `.exe`, or the asset lacks a browser download URL | Check the asset name and the API response |
| Button appears stuck | Browser script error or unexpected request behavior | Open browser developer tools and inspect Console and Network |
| Download starts but installer is wrong | The latest release contains an unintended `.exe` asset or wrong release contents | Correct the release assets and verify the latest release |

## Safe changes

If the release repository or asset naming convention changes, update the API URL, fallback URL, and asset selection logic together. Test both the direct-download path and fallback path.

Do not claim that the download was fully verified just because the browser was instructed to start it. The script triggers the download and displays a status message; it does not verify that the visitor saved or installed the file.
