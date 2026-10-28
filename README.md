# Bazooka Noodles — public site (home page + privacy policy + terms)

These static pages are the game's public home page and the privacy policy / terms URLs that
Google Play asks for. Google requires a publicly reachable page **on a domain whose ownership
you can verify by DNS** for the privacy policy and for developer/package verification; a
`raw.githubusercontent.com` URL or a bare `*.github.io` subdomain does not qualify.

`.gdignore` only keeps Godot from importing this folder into the game; it is not published.

## Hosting

GitHub Pages from the public repo `github.com/jayofelony/bn-branding`, custom domain
**`bazooka-noodles.xbitsnlgaming.com`** (Cloudflare: CNAME `bazooka-noodles` → `jayofelony.github.io`, proxy off so
GitHub can renew its certificate). The studio page at `https://www.xbitsnlgaming.com/` links here.

| File | Live URL |
|---|---|
| `index.html` | `https://bazooka-noodles.xbitsnlgaming.com/` |
| `privacy-policy.html` | `https://bazooka-noodles.xbitsnlgaming.com/privacy-policy.html` |
| `terms-of-service.html` | `https://bazooka-noodles.xbitsnlgaming.com/terms-of-service.html` |
| `app-ads.txt` | `https://bazooka-noodles.xbitsnlgaming.com/app-ads.txt` |
| `robots.txt` | `https://bazooka-noodles.xbitsnlgaming.com/robots.txt` |
| `sitemap.xml` | `https://bazooka-noodles.xbitsnlgaming.com/sitemap.xml` (add a page here when you add one) |
| `style.css`, `assets/…` | supporting files |

Contact address used in the pages: `support@xbitsnlgaming.com` (Cloudflare Email Routing,
forwarded to `oudshoorn.jeroen@gmail.com`).

## Publishing a change

1. Edit the pages here (this folder is the source copy).
2. Copy **every** file from this folder into the root of `bn-branding` and push to `main`.
   `CNAME` keeps the custom domain; a missing `CNAME` makes GitHub drop it.
   `app-ads.txt` must come along too: AdMob reads it from the Website field's domain. The same
   publisher line is at `https://www.xbitsnlgaming.com/app-ads.txt`; change both together.

## Domain verification (Google Search Console)

Sign in as `oudshoorn.jeroen@gmail.com` → **Add property → Domain** → `xbitsnlgaming.com`, add
the TXT record Google shows at Cloudflare and click **Verify**. A Domain property covers every
subdomain, which is what the Play and OAuth reviews check.

## Play Console

| Field | Value |
|---|---|
| App name | `Bazooka Noodles` |
| Package | `com.xbitsnl.bazookanoodles` |
| Website | `https://bazooka-noodles.xbitsnlgaming.com/` |
| Privacy policy | `https://bazooka-noodles.xbitsnlgaming.com/privacy-policy.html` |
| Email | `support@xbitsnlgaming.com` |

Store listing copy, Data safety answers and graphics are in `../store/`.

## Keeping it in sync

- **Logo, icon, feature graphic:** regenerate with `godot --path . --script tools/render_logo.gd`
  and copy from `assets/branding/` (`logo.png`, `icon_512.png` → `assets/icon.png`,
  `feature_graphic.png` → `assets/feature.png`, `splash_bg.png` → `assets/backdrop.png`).
- **Screenshots:** regenerate with
  `godot --path . --resolution 1920x1080 --script tools/store_screenshots.gd`
  and copy `store/screenshots/*.png` to `assets/screenshots/`.
- **Gameplay video** (`assets/video/`): a 22 s silent loop cut from a phone screen recording
  (0:24–0:46), 1280 px wide, MP4 (H.264) + WebM (VP9) + JPG poster, together ~3.5 MB. The full
  video with sound is on YouTube (`https://youtu.be/5Jnta__JhfM`), linked under the clip and used
  as the Play Store promo video. Re-cut with e.g.
  `ffmpeg -ss 24 -t 22 -i rec.mp4 -an -vf "fps=30,scale=1280:-2" -c:v libx264 -crf 26 -movflags +faststart gameplay.mp4`
  (WebM: `-c:v libvpx-vp9 -crf 36 -b:v 0`).
- **Feature-card art** (`assets/art/`): regenerate with
  `godot --path . --script tools/render_site_art.gd` when worms, weapons or skins change.
- **Privacy policy:** update it (and `../store/data-safety.md`) whenever an SDK is added or removed
  or new data leaves the device. It currently covers AdMob + UMP consent, Firebase Analytics,
  Crashlytics, Remote Config, In-App Messaging and Google Play Billing.
