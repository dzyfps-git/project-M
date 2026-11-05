# Mist: a calm, clean theme for Zen Browser

Mist is a theme (a "mod") for [Zen Browser](https://zen-browser.app). It keeps
Zen's layout and adds a soft violet-to-light-blue gradient, quieter chrome and
small, smooth animations. Nothing loud, nothing in the way.

## What it does

- **Active tab as a soft card.** The selected tab gets a faint gradient wash,
  an accent-tinted edge and a two-tone glow (violet on the left, blue on the
  right).
- **Quieter tab list.** Background tabs' titles are slightly dimmed. Favicons
  do a tiny spring "pop" on hover. Close buttons fade and spring in instead of
  appearing abruptly.
- **Quiet sidebar.** The bottom buttons and the "+ New Tab" row stay hidden
  until you hover the sidebar. They also stay visible while focus or an open
  menu is in the sidebar.
- **Floating page.** The website area gets a hairline edge and a softer,
  layered shadow.
- **Smooth tab switching.** The new page settles in with a short, subtle fade.
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

Mist isn't in the Zen Mods store yet, so for now you install it by hand with
`userChrome.css`:

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

| Pref | What it does | Store default |
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

## Installing it as a proper Zen mod (store)

The `mist` folder is already shaped like a Zen mod. `chrome.css` is the style,
`preferences.json` holds the settings shown in Zen's mod settings page
(including an accent-gradient dropdown and a radius box), and `readme.md` is the
store page. To publish it, submit it through the
[Zen theme store](https://github.com/zen-browser/theme-store). You'll need a
screenshot for the store image.

**Keep the mod's name exactly `Mist`.** Zen exposes dropdown settings on an
element whose id comes from the mod name (`#theme-Mist`), and the accent
presets in `chrome.css` look for that id.

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
