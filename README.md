# Handoff: note_dude — Landing & Donate Page

## Overview
A single-page marketing site for **note_dude**, a lightweight, keyboard-shortcut- and tag-driven note-taking app with todo features, styled to look like a terminal / TUI. The page introduces the product, demonstrates it via an animated mini-app, documents its keyboard map, tells the founder story, lists a changelog and FAQ, and provides a pay-what-you-want donate section. Audience: keyboard-loving technical users.

The live app it links to is at `https://app.notedude.app`.

## About the Design Files
The file in this bundle (`notedude Landing.html`) is a **design reference created in HTML** — a working prototype that shows the intended look, copy, and behavior. It is **not** meant to be shipped verbatim. The task is to **recreate this design in the target codebase's environment** using its established patterns (React/Next, Vue, Astro, plain HTML, etc.). If no codebase exists yet, choose an appropriate framework — given this is a static marketing page, a static-site approach (Astro, Next static export, plain HTML+CSS) is ideal. The animated demo is the only piece that needs real JS.

## Fidelity
**High-fidelity (hifi).** Final colors, typography, spacing, and interactions are all defined. Recreate the UI pixel-accurately using the values in the Design Tokens section. The only approximate parts are placeholder content (donate URLs, crypto addresses) which must be replaced with real values.

## Layout / Page Structure
Single long scrolling page, max content width **980px**, centered, 28px horizontal padding. Background is near-black `#0a0a0a` with a subtle purple radial glow at the top. Font is **Fira Code** (monospace) throughout. Vertical section rhythm: each `<section>` has `56px` top/bottom padding and a `1px` top border (`--border`).

Order of sections, top to bottom:
1. **Sticky top bar**
2. **Hero** (wordmark + tagline + meta)
3. **Animated demo terminal**
4. **Features** (`#features`)
5. **Keyboard cheatsheet** (`#keys`)
6. **Founder note** (`#why`)
7. **Changelog** (`#changelog`)
8. **FAQ** (`#faq`)
9. **Donate** (`#donate`)
10. **Footer**

### 1. Top bar
- Sticky, `position: sticky; top: 0`, z-index 50. Background `rgba(10,10,10,0.85)` with `backdrop-filter: blur(8px)`. Bottom border `1px solid --border`.
- Inner: flex space-between, 14px/28px padding, max 980px centered, font-size 13px.
- **Left (brand):** `>` in accent purple, then `note_dude` in bright fg (weight 500), then `v0.4.2` in dim fg.
- **Right (nav):** text links `features`, `keys`, `changelog`, `faq`, `donate` in `--fg-dim`, hover → `--fg-bright`. Then a CTA button **`open app →`** linking to `https://app.notedude.app`: 7px/14px padding, `1px solid --accent` border, text `--accent-bright`, bg `rgba(141,138,212,0.06)`, radius 2px. Hover → solid `--accent` bg with `#0a0a0a` text; the `→` arrow translates +2px on hover.
- Nav hidden below 720px (brand + CTA remain).

### 2. Hero
- Padding `64px 0 40px`.
- **Wordmark:** `> note_dude` — the `>` in `--fg-dim`, `note_dude` in `--accent`. Font-size **40px**, weight 600, letter-spacing -0.01em. Followed by a blinking block cursor (30px tall, accent-colored block, see cursor animation).
- **Tagline:** "notes for people who never let go of the keyboard." — `--fg-bright`, 19px, weight 500.
- **Sub:** "a lightweight, tag-driven notes & todo app shaped like a terminal. `sudo make-note` — no menus, no chrome, no mouse required." — `--fg-dim`, 14px, max-width 620px. The `sudo make-note` is inline accent-colored.
- **Meta row:** flex, 18px gap, 12px, `--fg-dim`. Items separated by `·` dots in `--fg-dimmer`: "● local-first" (bullet in `--ok` green), "~38kb gzipped", "works offline", "vim-style nav", "0 ads, 0 trackers".

### 3. Animated demo terminal
A faux app window that auto-plays a looping animation demonstrating note creation and search.
- **Frame:** `1px solid --border-bright`, radius 4px, bg `#060606`, large soft drop shadow (`0 20px 60px -20px rgba(0,0,0,0.8)`). Position relative (holds the key indicator).
- **Title bar:** bg `--bg-3`, bottom border `--border`, 8px/14px padding, 11.5px `--fg-dim`. Left: three 11px circle "dots" (bg `#2a2a28`, border `--border-bright`). Center: "note_dude — ~/notes". Right: "⌘? for help" in `--fg-dimmer`.
- **Search row:** 12px/16px padding, bottom border `1px dashed --border-bright`, min-height 42px. `>` in accent, then typed search text, then a blinking cursor, then placeholder "search notes..." in `--fg-dimmer`.
- **Body:** CSS grid `240px 1fr`, min-height 340px.
  - **Left list:** dashed right border. Each note row: 8px/16px padding. Title (13.5px, weight 500, `--fg-bright`, ellipsized) + meta line (12px, `--fg-dim`, ellipsized; `#tags` rendered in accent). Selected note: bg `--accent-bg` (`#2c2b58`), brighter text.
  - **Right detail:** 18px/22px padding. Title (15px, weight 500) + body (13px, line-height 1.7, `white-space: pre-wrap`). In the body, `#tags` render in accent and `[x]`/`[ ]` render as `☑`/`☐` (done items struck through in `--fg-dim`).
- **Key indicator:** absolutely positioned bottom-right pill, `rgba(141,138,212,0.12)` bg, `1px solid --accent`, `--accent-bright` text, 6px/12px, radius 3px, fades in/out (`opacity` 0↔1) to announce each keystroke (e.g. "⌘N · new note").

### 4. Features (`#features`)
- Section label: `## features` (the `##` in accent). Title: "built around the home row." (22px, weight 500, `--fg-bright`).
- **Grid:** 2 columns, `1px` gap over a `--border` background with a `--border` outer border + radius 4px → produces hairline dividers between cells. Each cell bg `--bg`, 22px/24px padding. (1 column below 720px.)
- 6 features, each: head row = accent number `01.`–`06.` + name (15px, weight 500, `--fg-bright`); then description (13px, `--fg-dim`, line-height 1.65). Inline `code` spans are accent text on `--accent-bg-soft` bg, 1px/6px, radius 2px.
- Content (exact):
  1. **keyboard, all the way down** — "every action has a shortcut. nothing requires a mouse. press `?` any time to see what's bound. yes, `hjkl` works."
  2. **tags are first-class** — "type `#anything` mid-note and it becomes a tag. nest them like `#work/standup`. filter the whole library by typing the tag in search."
  3. **find as fast as you type** — "fuzzy search across titles, bodies, and tags. press `/` from anywhere. results re-rank as you go. arrow keys to pick, enter to open."
  4. **todos that live inside notes** — "type `[]` to start a checkbox. `⌘E` toggles. todos roll up into a unified `#todo` view. no separate app, no separate brain."
  5. **local-first, sync optional** — "notes live in your browser's storage. nothing leaves your device unless you turn on sync. import / export to plain markdown — your data, your problem."
  6. **command palette** — "`⌘K` opens a single text input that runs everything: jump to a note, run a command, change a setting. you'll never need a menu again."

### 5. Keyboard cheatsheet (`#keys`)
- Label `## reference`, title "the entire keyboard map."
- Container: `1px solid --border`, radius 4px. Divided into 4 **sections**, each with a header bar (bg `--bg-3`, `--fg-dim`, 12px, e.g. `~/notes · navigation` where `~` is accent) and rows.
- Each **row:** grid `200px 1fr`, 6px/16px padding, 13px. Hover bg `--bg-2`. Left = key combo (one or more `.key` chips); right = description in `--fg-dim`. (Stacks to 1 column below 720px.)
- **Key chip:** inline-block, 1px/7px padding, bg `--bg-3`, `1px solid --border-bright`, radius 3px, `--fg-bright`, 12px weight 500, min-width 22px centered. A "plus" variant renders the `+`/`/` separators as borderless dim text.
- Sections & rows:
  - **navigation:** `/` focus search · `⌘ + K` command palette · `j / k` next/prev note · `gg / G` first/last note · `Esc` leave search / close palette
  - **editing:** `⌘ + N` new note · `⌘ + D` delete note · `⌘ + E` toggle todo · `⌘ + P` pin/unpin · `⌘ + ]` indent · `⌘ + [` outdent
  - **tags & filters:** `#` start a tag · `⌘ + T` add tag · `⌘ + ⇧ + F` filter library by tag
  - **window:** `⌘ + \` toggle sidebar · `⌘ + ,` settings · `?` show cheatsheet anywhere

### 6. Founder note (`#why`)
- Label `## why this exists`, title "a note from the dude."
- Card: bg `--bg-2`, `1px solid --border`, **3px left border in `--accent`**, radius `0 4px 4px 0`, 28px/32px padding.
- Head: `> cat ~/why.md` (accent) · `|` (dimmer) · "last edited: a tuesday" (dim).
- 4 paragraphs (14px, `--fg`, line-height 1.75, max-width 70ch) telling the build story; inline `code` accent spans for `todo.txt` and `sudo make-note`. Sign-off: "— **the dude** · `$` whoami: a person with too many notes".

### 7. Changelog (`#changelog`)
- Label `## changelog`, title "tail -f CHANGELOG.md".
- Each entry: grid `130px 1fr`, 24px gap, 14px/0 padding, bottom border `--border`.
  - Left: version (accent, weight 500) + date (12px dim).
  - Right: bulleted list, no markers; custom prefixes via `::before`: additions `+ ` in `--ok` green, fixes (`.fix`) `~ ` in `--warn` amber, removals (`.rm`) `- ` in `--err` red. Inline `code` in accent.
- 5 entries: v0.4.2 (today), v0.4.1 (3 days ago), v0.4.0 (last week), v0.3.0 (3 weeks ago), v0.2.0 (last month). See HTML for exact bullet copy.

### 8. FAQ (`#faq`)
- Label `## faq`, title "man note_dude".
- Container `1px solid --border`, radius 4px. One item, 20px/24px padding:
  - Q: "`>` is there an MCP?" (`>` accent; 15px weight 500 `--fg-bright`).
  - A: "of course." (`--fg-dim`, 14px, left-padded 24px to align under the question text).

### 9. Donate (`#donate`)
- Section has an extra purple radial glow at its top.
- Label `## donate`, title "pay what you want, if you want."
- Intro (14px, `--fg`, max 65ch): "note_dude is free and will stay free. **no paywall, no premium tier, no "pro" features.** if it's earned a spot in your daily flow…" (the middle clause in accent).
- **Amount buttons:** grid of 4 (2 cols below 720px), 10px gap. Each button: bg `--bg-2`, `1px solid --border-bright`, radius 3px, 16px/12px padding. Big amount (17px, weight 500) over a small label (11px, `--fg-dim`). Hover → accent border + accent-bright text + faint accent bg. **Selected** state: accent border, `rgba(141,138,212,0.12)` bg, accent text. Default selected = $9.
  - `$3` a coffee · `$9` a real meal · `$27` a domain renewal · `$81` absurdly generous
- **Custom amount:** "or:" label + an input wrap (bg `--bg-2`, border `--border-bright`, focus-within → accent border) containing an accent `$` and a number input (placeholder "any number that feels right").
- **Providers grid:** 2 cols (1 below 720px), hairline dividers like the features grid. Each provider = flex space-between: name (`--fg-bright`, 14px, weight 500) + meta (11.5px dim), and an accent arrow that translates +3px on hover.
  - **GitHub Sponsors** → `https://github.com/sponsors/notedude` — "recurring · matched by github for new sponsors"
  - **Buy Me a Coffee** → `https://buymeacoffee.com/notedude` — "one-time · no account required"
  - **PayPal** → `https://paypal.me/notedude` — "one-time · works almost everywhere"
  - **Crypto** → toggles the crypto block (arrow is `↓`/`↑`) — "BTC · ETH · click to reveal addresses"
- **Crypto block** (hidden until toggled): bordered, two rows grid `80px 1fr auto`: coin (accent), address (mono, ellipsized), and a **copy** button. Copy writes the address to clipboard, then shows "copied ✓" in `--ok` green for 1.4s.

### 10. Footer
- Top border, 32px/0 40px padding, 12px `--fg-dim`. Flex space-between (wraps).
- Left: "`>` built with ♥ and too much coffee · © 2026 note_dude" (`>` and ♥ in accent).
- Right links: app, changelog, github, hi@notedude.app.

## Interactions & Behavior

### Demo animation (the main piece of real JS)
An infinite loop (`runDemo()`) driven by `async/await` + `sleep(ms)`. One cycle:
1. Reset to 8 seeded notes, empty search, no selection. Wait 1.4s.
2. Show key indicator "⌘N · new note" (0.7s). Insert a new selected "New Note" at top of list. Clear detail title/body.
3. Type the title "lunch w/ sam" character-by-character (~70ms/char + jitter) into the detail title, with a trailing typing cursor; mirror the title into the list row.
4. Type a multi-line body (~32ms/char) with live rendering: `#personal` becomes an accent tag span; update the list row meta to `10:28 AM | #personal`.
5. Show "/ · search" indicator, then type `#personal` into the search field; filter the list to matching notes only. Hold 1.8s.
6. Show "Esc · back to library", clear search, restore full list.
7. Show "⌘K · command palette" briefly, then loop.
- **Typing cursor** and the two **block cursors** (search + hero wordmark) use a `blink` keyframe: `@keyframes blink { to { background: transparent; } }` at `1.1s steps(2, start) infinite`.
- In the prototype the demo starts immediately on load. (An earlier IntersectionObserver gate was removed — start unconditionally.)
- Rendering helpers: `tagify()` wraps `#tag` matches in `<span class="tag">`; `renderTodos()` converts `[x]`/`[ ]` line starts to `☑`/`☐` with strike-through on done.

### Donate amount selection
- Clicking an amount button clears `.selected` from all and sets it on the clicked one, and clears the custom input.
- Typing in the custom input clears `.selected` from all amount buttons.

### Crypto reveal & copy
- Clicking the **Crypto** provider toggles `#crypto-block` display and swaps its arrow `↓`↔`↑` (preventDefault on the anchor).
- Copy buttons use `navigator.clipboard.writeText`; on success show "copied ✓" + `.copied` (green) for 1.4s; on failure fall back to "select & copy".

### General
- All in-page nav links are anchor hrefs to section IDs (smooth scroll optional — not currently set; CSS `scroll-behavior: smooth` is a safe addition). **Do not use `scrollIntoView`.**
- Hover transitions are ~0.15s on color/background/transform.

## State Management
Minimal — this is a marketing page. For a component framework:
- **Demo:** an animation controller (could be a custom hook / effect with cancellation on unmount). Holds: list of notes (with `title`, `meta`, `body`, `selected`), current detail title/body, search string, key-indicator text/visibility. Drive it off a timeline rather than deeply nested timeouts if you can (e.g. an array of steps). Make sure to clear timers on unmount.
- **Donate:** `selectedAmount` (one of the presets or `custom`), `customAmount` string, `cryptoOpen` boolean, transient `copied` flag per address.
- No data fetching. No backend in the design (donate links are external; wire real provider URLs).

## Design Tokens
```
/* color */
--bg:            #0a0a0a   /* page background */
--bg-2:          #0f0f0f   /* cards, inputs, hover */
--bg-3:          #161616   /* title bars, key chips, section heads */
--fg:            #d8d8d2   /* body text */
--fg-bright:     #ececea   /* headings, emphasis */
--fg-dim:        #9a9a92   /* secondary/meta text */
--fg-dimmer:     #5a5a55   /* faint text, separators */
--accent:        #8d8ad4   /* primary purple (from app screenshot) */
--accent-bright: #a6a3e6   /* accent hover/emphasis */
--accent-bg:     #2c2b58   /* selected note background */
--accent-bg-soft:#1c1b3a   /* inline code background */
--border:        #1f1f1d   /* hairline borders, grid gaps */
--border-bright: #2c2c2a   /* stronger borders, chips */
--warn:          #d0b070   /* changelog fix (~) */
--ok:            #8fbf8c   /* changelog add (+), copied, status bullet */
--err:           #c97a7a   /* changelog removal (-) */

/* type */
font-family: 'Fira Code', ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace;
base font-size: 14px; line-height: 1.55; weight 400; font-variant-ligatures: contextual;
hero wordmark: 40px / 600
tagline: 19px / 500
section title: 22px / 500
feature/faq name: 15px / 500
body/desc: 13–14px
meta/labels: 11.5–12px
key chips / code: 12px

/* radius */
2px  — CTA, inline code, copy chip
3px  — key chips, amount buttons, key indicator, inputs
4px  — cards, grids, frames

/* shadow */
demo frame: 0 20px 60px -20px rgba(0,0,0,0.8), 0 0 0 1px rgba(141,138,212,0.05)

/* layout */
content max-width: 980px; horizontal padding: 28px
section padding: 56px 0; top border 1px --border
breakpoint: 720px (collapse multi-col grids, hide top nav)
selection: background --accent-bg, color --fg-bright
```

## Assets
- **No image assets.** All visuals are CSS + text. The logo is a text wordmark (`> note_dude`), not an image.
- **Font:** Fira Code loaded from Google Fonts (weights 300–700). In a real codebase prefer self-hosting (e.g. `@fontsource/fira-code`) for performance/offline.
- Symbols used: `→ ↓ ↑ ● ♥ ☑ ☐ ⌘ ⇧` (Unicode, no icon library needed).

## Placeholders to replace before shipping
- Donate provider URLs: `github.com/sponsors/notedude`, `buymeacoffee.com/notedude`, `paypal.me/notedude` — confirm real handles.
- Crypto addresses (BTC `bc1q…`, ETH `0x…`) are fake — replace with real wallet addresses.
- Email `hi@notedude.app`, github `github.com/notedude`, version `v0.4.2`, and changelog dates/copy.

## Files
- `notedude Landing.html` — the complete single-file prototype (HTML + CSS in a `<style>` block + vanilla JS in `<script>` blocks). Everything described above lives here; use it as the source of truth for exact copy and values.
