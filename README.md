# Mist: a calm, clean theme for Zen Browser

Mist is a theme (a "mod") for [Zen Browser](https://zen-browser.app). It keeps
Zen's layout and adds a soft violet-to-light-blue gradient, quieter chrome and
small, smooth animations. Nothing loud, nothing in the way.

## What it does

- **Active tab as a soft card.** The selected tab gets a gradient wash, a
  violet-to-blue edge and a two-tone glow (violet on the left, blue on the
  right). A soft band of light sweeps across it once as it becomes active.
- **Tabs that react.** Hovering a tab tints it faintly violet, and while a page
  loads, a gentle shimmer loops across its tab.
- **Quieter tab list.** Background tabs' titles are slightly dimmed. Favicons
  do a tiny spring "pop" on hover. Close buttons fade and spring in instead of
  appearing abruptly.
- **Quiet sidebar.** The bottom buttons and the "+ New Tab" row stay hidden
  until you hover the sidebar. They also stay visible while focus or an open
  menu is in the sidebar.
- **Floating page.** The website area gets a hairline edge and a softer,
  layered shadow.
- **URL bar bloom.** The floating URL bar fades in with a gentle spring and a
  violet/blue glow, and the results slide down a few pixels.
- **Essentials.** The tiles lift slightly on hover, and the active one gets the
  gradient ring and glow.
- **Folders that read as groups.** An open folder (Zen's tab groups) sits on a
  faint violet-tinted tray, and folder rows match the tab style.
- **Favicon pop.** When a tab becomes active, its icon does a tiny spring pop.
- **Favicon glow (experimental, off by default).** The active tab's icon glows
  in its own colors, multi-color icons included. CSS can't read an icon's
  color, so this uses an SVG filter that blurs a copy of the icon behind
  itself.
- **Hidden space name.** The space name at the top of the tab list is hidden by
  default for a cleaner sidebar. You can still switch spaces with the icons at
  the bottom, swipes or shortcuts.
- **Small touches.** Zen's page-loading bar uses the gradient. Toolbar buttons
  have a tactile press. Menu items are rounder and fade on hover.
- **Respects your system.** If your OS asks for reduced motion, Mist turns its
  animations off. Light and dark mode are both tuned.

## Install

### With Sine (recommended: updates itself)

[Sine](https://github.com/CosmoCreeper/Sine) is a mod manager for Zen. It
installs mods straight from a GitHub repo and pulls updates from it, so you
never have to copy files again.

1. Install Sine using the installer from its
   [releases page](https://github.com/CosmoCreeper/Sine/releases/latest), then
   restart Zen.
2. Open Zen's **Settings** and go to Sine's page.
3. In the box under "add your own locally from a GitHub repo", type
   `dzyfps-git/project-M` and click **Install**.
4. Under **Installed Mods**, open Mist's settings once. Sine applies the
   default settings (quiet sidebar, hidden space name) the first time you do.

Sine only has two requirements for this repo: it must be **public**, and the
mod must live on the **`main`** branch.

### By hand (userChrome.css)

If you'd rather not use Sine:

1. In Zen, open `about:config` and set
   `toolkit.legacyUserProfileCustomizations.stylesheets` to `true`.
2. Open `about:support`. Next to **Profile Folder**, click **Open Folder**.
3. In that profile folder, create a folder named `chrome` if there isn't one.
4. Copy this repo's `mist` folder into it, so that you end up with
   `chrome/mist/chrome.css`.
5. In `chrome/`, create a file named `userChrome.css` (or open the one that's
   already there) and put this line at the **very top**:

   ```css
   @import url("mist/chrome.css");
   ```

6. Restart Zen.

To uninstall, remove that line (or the `mist` folder) and restart.

### Settings when installed by hand

The on/off settings are regular Zen prefs. In `about:config`, search for the
name, choose **Boolean**, and click **+**:

| Pref | What it does | Default with Sine |
| --- | --- | --- |
| `mod.mist.quiet_sidebar` | Hide the bottom buttons and New Tab row until you hover the sidebar | on |
| `mod.mist.hide_space_name` | Hide the space name at the top of the tab list | on |
| `mod.mist.compact_tabs` | Shorter tab rows | off |
| `mod.mist.hide_close` | Hide tab close buttons (middle-click or Ctrl/Cmd+W still work) | off |
| `mod.mist.favicon_glow` | The active tab's icon glows in its own colors (experimental) | off |
| `mod.mist.flat_page` | Remove the floating shadow around websites | off |
| `mod.mist.no_glow` | Turn off the accent glows | off |
| `mod.mist.no_motion` | Turn off Mist's animations | off |

With a hand install, every pref starts **off** until you create it. So if you
want the quiet sidebar and the hidden space name, add
`mod.mist.quiet_sidebar` = `true` and `mod.mist.hide_space_name` = `true`.

### Changing the colors or roundness by hand

Add a rule to `userChrome.css` **below** the `@import` line:

```css
:root {
  --mist-a: #9b87ff;         /* gradient start (violet) */
  --mist-b: #6cc8ff;         /* gradient end (light blue) */
  --mod-mist-radius: 12px;   /* roundness of tabs, tiles and menus */
}
```

Some pairs to try:

- Aurora: `#34d399` → `#3b9eff`
- Sunset: `#ff7aa2` → `#ffb35c`
- Follow your space color: `var(--zen-primary-color)` →
  `oklch(from var(--zen-primary-color) l c calc(h + 45))`

## Updating Mist

Edit anything in `mist/` and push it to `main`. That's it.

A GitHub Action (`.github/workflows/stamp-update.yml`) then stamps a fresh
`updatedAt` time into `theme.json`. That's the field Sine checks. Everyone
using Mist through Sine gets the update on their next update check (or right
away with **Check for Updates**). The action commits to `main`, so pull before
your next edit if you work from a local copy.

## Publishing to the Sine store

Once the repo is public, anyone can install Mist by repo name. To also show
up in the [Sine marketplace](https://sineorg.github.io/store/):

1. Add a real screenshot of Mist in Zen, and put its URL in `theme.json` as
   `"image"`.
2. Open an issue on [sineorg/store](https://github.com/sineorg/store/issues/new/choose)
   using the **Add Theme** template, with this repo's URL.

After that, the store re-syncs from this repo on its own schedule, so the
"edit and push" flow above still applies.

`theme.json` is the mod's metadata. It sets `"ai": "yes"` because the Sine
store asks mods to disclose AI involvement, and Mist was written with an AI
assistant.

**Keep the mod's name exactly `Mist`.** Zen and Sine both expose dropdown
settings on an element whose id comes from the mod name (`#theme-Mist`), and
the accent presets in `chrome.css` look for that id.

### The official Zen Mods store

Mist can go in Zen's own store too, through the
[Zen theme store](https://github.com/zen-browser/theme-store). There, each
update goes through that store's review process instead of coming straight
from this repo, which is why Sine is the easier route for frequent updates.

## Tweaking it live

Zen's UI is just CSS, so you can inspect it the way you'd inspect a website:

1. In `about:config`, set `devtools.chrome.enabled` and
   `devtools.debugger.remote-enabled` to `true`.
2. Press **Ctrl+Shift+Alt+I** (**Cmd+Opt+Shift+I** on macOS) to open the
   Browser Toolbox. Use its element picker on any part of the UI.
3. Edit `chrome/mist/chrome.css` and restart Zen to see the changes.

## Status

Mist was written against Zen's current source code (the selectors, settings
system and animations it hooks into were all checked there). It has **not
yet been run inside a live Zen window**. If anything looks off, inspect it with
the Browser Toolbox, or open an issue with a screenshot.

The favicon glow is the most experimental part. It relies on Firefox loading an
SVG filter from a `data:` URL, which couldn't be confirmed without a running
Zen. If icons look wrong or disappear with it on, turn it back off.
