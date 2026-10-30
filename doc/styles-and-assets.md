# Styles and assets

## Styling approach

All CSS currently lives in the `<style>` element inside `index.html`. There is no separate stylesheet or build pipeline in the checked-in page source.

The design uses a dark background, pale text, and a lime accent. Shared color and layout values are CSS custom properties near the top of the stylesheet:

- `--bg`: page background.
- `--panel` and `--panel-soft`: panel surfaces.
- `--text` and `--muted`: primary and secondary text.
- `--accent` and `--accent-ink`: lime accent and text used on it.
- `--line`: borders.
- `--max`: maximum content width.

When changing the theme, start with these variables instead of replacing colors one selector at a time.

## Main layout patterns

- `.wrap` centers content and constrains its width.
- `.topbar` and `.nav` arrange the brand and navigation.
- `.hero`, `.actions`, and `.product-shot` control the first-screen content.
- `.trust-strip` and `.trust-item` present factual privacy information in compact institutional cards.
- `.download-frame` groups the official release action and its source/backup context.
- `.download-dialog` and `.dialog-*` style the deliberate pre-download confirmation step.
- `.grid` and `.feature` arrange the feature cards.
- `.manifesto` creates the two-column privacy panel.
- `.notice` styles the installation warning.
- `.faq` and `details` style expandable questions.
- `.closing` styles the final call to action.
- `.footer-inner` arranges the footer content.

Use the existing class patterns where possible so sections remain visually consistent.

## Responsive behavior

The stylesheet includes breakpoints at 760px and 520px.

- At widths up to 760px, the feature grid becomes two columns and the privacy panel becomes one column.
- At widths up to 520px, the feature grid becomes one column, action buttons fill the available width, and the footer stacks vertically.
- The CSS also respects `prefers-reduced-motion: reduce` to minimize transitions and disable smooth scrolling for visitors who request reduced motion.

When changing spacing, font sizes, or columns, test both desktop and narrow mobile widths. Do not test only by resizing the desktop window once; verify that the page has no horizontal overflow and that links/buttons remain usable.

## Image and icon references

The HTML references these paths:

| Reference in the page | Purpose |
|---|---|
| `imgs/logo.png` | Logo displayed in the header |
| `imgs/logo.ico` | Browser favicon |
| `imgs/Screenshot%202026-09-04%20081020.png` | Main product screenshot |
| `imgs/BMTB_demo.png` | Open Graph/social preview image |

The screenshot filename contains spaces, so the URL in HTML encodes them as `%20`. If you rename the file, update the HTML path as well.

Keep images optimized and provide meaningful alternative text for informative screenshots. The small header logo has an empty `alt` because the adjacent brand text already names the product.

## Accessibility details already present

The current page includes several useful accessibility choices:

- A `lang="en"` document declaration.
- A viewport meta tag for mobile layouts.
- Visible keyboard focus styles for links and buttons.
- A labeled main navigation region.
- Alternative text for the product screenshot.
- `aria-live="polite"` for download status updates.
- `aria-busy` during the download lookup.
- Native `details`/`summary` controls for the FAQ.
- Reduced-motion CSS.

Preserve these when editing. If you add an interactive element, ensure it can be reached and used by keyboard and that its state is communicated accessibly.


## Security and trust presentation

The security cues are intentionally descriptive rather than certification badges. The page states that notes are stored locally, that password/encryption protection is handled by the desktop app, and that no hosted notes account is required. It does not claim an independent security audit, certification, guaranteed protection, or a secure website checkout.

The download frame visually groups the action with the official GitHub release destination. Both download buttons open the same native HTML dialog. The visitor must type `DOWNLOAD` before the existing GitHub release lookup starts. The dialog can be dismissed with its cancel button or the browser's native Escape behavior.

Do not remove or weaken the installation warning without checking current release behavior. The confirmation exists because the current release may overwrite an older notes database and does not provide password recovery.
