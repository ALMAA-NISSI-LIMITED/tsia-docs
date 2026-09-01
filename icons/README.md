# TSIA app icon pack

Every icon uses the **full TSIA lockup** — wordmark, pin and road — on a white
ground. The standalone A symbol is retired and appears nowhere in this pack.

## Contents
- `ios/` — all AppIcon sizes + `Contents.json`. Drop into
  `Assets.xcassets/AppIcon.appiconset/`. `-dark` and `-tinted` cover iOS 18 icon modes.
- `android/mipmap-*/` — legacy launcher + round launcher.
- `android/adaptive/` — 432px foreground / background / monochrome (Themed Icons, Android 13+).
  Lockup sits inside the 66% safe zone so no OEM mask clips it.
- `web/` — favicons 16→512, multi-res `favicon.ico`, apple-touch-icon, PWA icons +
  maskable pair, Windows tiles, `site.webmanifest`, `browserconfig.xml`, `head-snippet.html`.
- `social/` — 1200×630 OG images (light + navy) and 400px avatars.

## Known trade-off
The lockup is ~2.08:1, so inside a square it fills about 41% of the height and
leaves empty bands top and bottom. Below 48px the letterforms fall under the
24px minimum in the brand guide; those sizes render the lockup in solid
#0E1B2A navy so the silhouette stays as legible as possible. Expect the favicon
at 16px to read as a dark bar rather than as letters — this is inherent to using
a wide lockup in a square slot, not a generation fault.

## Colors used
Ground #FFFFFF (dark variants #0E1B2A) · Green #00873E / #2FD36A on dark · Navy #0E1B2A
