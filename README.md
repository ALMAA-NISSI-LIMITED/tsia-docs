# TSIA Brand Guide

Visual design system for **Transport Systems Infrastructure Africa** — the Kenyan ride-hailing platform covering the admin dashboard, Flutter mobile apps (Rider & Driver), customer web SPA (tsiarides.net), and developer tooling.

**Live guide → [https://almaa-nissi-limited.github.io/tsia-docs/brand-guide.html](https://almaa-nissi-limited.github.io/tsia-docs/brand-guide.html)**

---

## What's in the guide

| Section | What it covers |
|---|---|
| Color | Brand palette + semantic status colors |
| Typography | DM Sans (admin/docs), Poppins (mobile + web SPA), DM Mono (data) |
| Typography · Web | Poppins display scale for tsiarides.net — display-1 through lead |
| Spacing & Radius | 8pt grid, marketing spacing tokens, touch-target minimum |
| Shadows | Navy-tinted elevation ramp (sm → xl) |
| Icons | Material Symbols (Flutter), Lucide React (admin), Remix (Blade) |
| App Icon Pack | iOS, Android, Web favicons, PWA, social OG images |
| Components | Buttons, badges, cards, inputs |
| Mobile · Splash | Rider app splash — "Go Anywhere" lockup |
| Mobile · Rider App | Core screens: Home map, Route search, Activity, Account |
| Mobile · Activity | 5-screen ride history & support flow |
| Mobile · Account | 5-screen profile, payment, safety & saved places flow |
| Motion | Timing tokens + easing |
| Voice & Tone | Copy rules for Kenyan riders, drivers, and operators |
| Admin SCSS | Laravel dashboard variable quick reference |
| LLM Instructions | Copy-paste brand prompts for Claude/Cursor/Copilot |

## Repo structure

```
tsia-docs/
├── brand-guide.html        # Single-file design system (self-contained)
├── icons/                  # App icons — iOS, Android, web, social
│   ├── ios/
│   ├── android/
│   ├── web/
│   └── social/
├── rider-screen-*.png      # Rider app UI screenshots
├── auth-screen-*.png       # Auth & onboarding flow screenshots
├── activity-screen-*.png   # Activity & ride history screenshots
├── account-screen-*.png    # Account & settings screenshots
└── tsia-splash.png         # Legacy splash (superseded by rider-screen-splash.png)
```

## Contributing

All documentation lives in `brand-guide.html`. Edit it directly — no build step needed.

Screenshots go in the repo root. Follow the naming convention:
- `rider-screen-<name>.png` — Rider app screens
- `driver-screen-<name>.png` — Driver app screens (future)

---

ALMAA NISSI LIMITED · 2026
