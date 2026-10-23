# Bazooka Noodles — public site (home page + privacy policy + terms)

These static pages are the game's public home page and the privacy policy / terms URLs that
Google Play asks for. Google requires a publicly reachable page **on a domain whose ownership
you can verify by DNS** for the privacy policy and for developer/package verification; a
`raw.githubusercontent.com` URL or a bare `*.github.io` subdomain does not qualify.

Target: host these at **`https://bazooka-noodles.evemarketscanner.com/`** (same setup as Kings
and Fillomino; `evemarketscanner.com` is already verified in Google Search Console).

## Files

| File | Live URL |
|---|---|
| `index.html` | `https://bazooka-noodles.evemarketscanner.com/` |
| `privacy-policy.html` | `https://bazooka-noodles.evemarketscanner.com/privacy-policy.html` |
| `terms-of-service.html` | `https://bazooka-noodles.evemarketscanner.com/terms-of-service.html` |
| `app-ads.txt` | `https://bazooka-noodles.evemarketscanner.com/app-ads.txt` |
| `style.css`, `assets/…` | supporting files (logo, icon, feature graphic, screenshots, font) |

`app-ads.txt` authorises Google AdMob for this app. Its publisher line must stay identical to the
copies on the Kings site and in the `eve-market-scanner` repo (`static/app-ads.txt`, apex domain).
`.gdignore` only keeps Godot from importing this folder into the game; it is not published.

Contact address used in the pages: `oudshoorn.jeroen@gmail.com` (swap for a branded support
address later if you set one up).

## Step 1 — publish the files (GitHub Pages)

1. The public repo is `github.com/jayofelony/bn-branding`.
2. Copy the contents of this `site/` folder into the **root** of that repo and push to `main`.
   Copy **every** file, `app-ads.txt` included: AdMob reads it from this domain.
3. Repo → **Settings → Pages → Source: "Deploy from a branch" → `main` / `(root)`**.
4. Same page → **Custom domain** → `bazooka-noodles.evemarketscanner.com` → Save.
   GitHub adds a `CNAME` file to the repo and provisions HTTPS once DNS resolves.

## Step 2 — DNS (for evemarketscanner.com)

```
Type   Name             Value
CNAME  bazooka-noodles  jayofelony.github.io.
```

Wait until it resolves, check that `https://bazooka-noodles.evemarketscanner.com/` loads, and
enable **Enforce HTTPS** in the Pages settings.

## Step 3 — Google Search Console

The **Domain** property `evemarketscanner.com` (verified by DNS for Kings) already covers every
subdomain, including `bazookanoodles.`. Nothing to add.

## Step 4 — Play Console

| Field | Value |
|---|---|
| App name | `Bazooka Noodles` |
| Package | `com.xbitsnl.bazookanoodles` |
| Website | `https://bazooka-noodles.evemarketscanner.com/` |
| Privacy policy | `https://bazooka-noodles.evemarketscanner.com/privacy-policy.html` |
| Email | `oudshoorn.jeroen@gmail.com` |

Store listing copy, Data safety answers and graphics are in `../store/`.

## Keeping it in sync

- **Logo, icon, feature graphic:** regenerate with `godot --path . --script tools/render_logo.gd`
  and copy from `assets/branding/` (`logo.png`, `icon_512.png` → `assets/icon.png`,
  `feature_graphic.png` → `assets/feature.png`, `splash_bg.png` → `assets/backdrop.png`).
- **Screenshots:** regenerate with
  `godot --path . --resolution 1920x1080 --script tools/store_screenshots.gd`
  and copy `store/screenshots/*.png` to `assets/screenshots/`.
- **Privacy policy:** update it (and `../store/data-safety.md`) whenever an SDK is added or removed
  or new data leaves the device. It currently covers AdMob + UMP consent, Firebase Analytics,
  Crashlytics, Remote Config, In-App Messaging and Google Play Billing.
