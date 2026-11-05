# Mist: a calm, glassy theme for Zen Browser

Mist is a theme (a "mod") for [Zen Browser](https://zen-browser.app). It keeps
Zen's layout and makes it frosted glass: translucent surfaces, hairline edges,
quieter chrome and small, smooth animations. The theme stays neutral and lets
your pages and icons bring the color.

## What it does

- **A glass active tab.** The selected tab is a pane of frosted glass with a
  hairline edge. When you switch to it, a soft wave of light glides across it
  once. No glow, no colored outline.
- **Tabs that react.** Hovering a tab gives it a faint glass highlight, and
  while a page loads, a gentle shimmer loops across its tab.
- **Mute from the favicon.** A playing tab shows a tiny animated equalizer on
  its favicon instead of Zen's separate speaker button. Hover the favicon and
  it becomes a mute/unmute button; click to toggle. Muted tabs show flat bars.
- **Quieter tab list.** Background tabs' titles are slightly dimmed. Favicons
  do a tiny spring "pop" on hover and when a tab becomes active. Close buttons
  fade and spring in instead of appearing abruptly.
- **Quiet sidebar.** The bottom buttons and the "+ New Tab" row stay hidden
  until you hover the sidebar. They also stay visible while focus or an open
  menu is in the sidebar.
- **Hidden space name.** The space name at the top of the tab list is hidden by
  default for a cleaner sidebar. You can still switch spaces with the icons at
  the bottom, swipes or shortcuts.
- **Glass media player.** The player card is frosted glass that blurs what's
  behind it (including the other cards in the stack). Play/pause is a small
  glass disc, the progress bar is a clean fill that thickens under the pointer
  with a white handle, and every control gets a round hover background and a
  springy press.
- **Folders that read as groups.** An open folder (Zen's tab groups) sits on a
  faint glass tray, and folder rows match the tab style.
- **Essentials.** Clean glass tiles that lift slightly on hover. Optionally,
  the active tile can hold its icon's colors, slowly drifting inside it.
- **Floating page.** The website area gets a hairline edge and a softer,
  layered shadow.
- **URL bar bloom.** The floating URL bar fades in with a gentle spring, and
  the results slide down a few pixels.
- **Small touches.** Toolbar buttons have a tactile press. Menu items are
  rounder and fade on hover.
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
| `mod.mist.essentials_color` | Let the active Essentials tile's icon colors drift inside it | off |
| `mod.mist.classic_audio` | Keep Zen's speaker button on playing tabs instead of the favicon mute control | off |
| `mod.mist.flat_page` | Remove the floating shadow around websites | off |
| `mod.mist.no_motion` | Turn off Mist's animations | off |

With a hand install, every pref starts **off** until you create it. So if you
want the quiet sidebar and the hidden space name, add
`mod.mist.quiet_sidebar` = `true` and `mod.mist.hide_space_name` = `true`.

The two dropdowns (accent and active tab motion) only exist in the mod
settings, not in `about:config`. With a hand install you get their defaults:
neutral glass, and a single wave when you switch tabs.

### Changing the accent or roundness by hand

The accent only colors two small things: Zen's page-loading bar and the media
progress bar. Add a rule to `userChrome.css` **below** the `@import` line:

```css
:root {
  --mist-a: #9b87ff;         /* accent start (violet) */
  --mist-b: #6cc8ff;         /* accent end (light blue) */
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

The favicon mute control reuses Firefox's own sound badge on the favicon, so
clicking it should mute and unmute the tab the same way Firefox does. If it
doesn't in your Zen version, turn on "Keep Zen's speaker button" to get the
original back.
