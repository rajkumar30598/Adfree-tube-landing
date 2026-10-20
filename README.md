# AdFree Tube — website

Landing page for AdFree Tube, served with GitHub Pages:
**https://rajkumar30598.github.io/Adfree-tube-landing/**

- `index.html` — the page (no build step). It reads `remote-config.json` to show the version and size.
- `.github/workflows/pages.yml` — deploys the site on every push to `main` (and on each published release). It copies the newest release's APK into the site as `AdFree-Tube.apk`.
- `remote-config.json` — read by the app at start-up. Edit it here to push fixes or messages to every user without an update:
  - `latestVersion` / `latestNotes` / `apkSize` / `releasedAt` / `updateUrl` — shows an "update available" banner to older versions
  - `minVersion` — forces an "update needed" banner
  - `notice` — a one-off message (`id`, `title`, `message`, optional `url`/`button`)
  - `clients`, `trendingQueries`, `pipedInstances` — hotfixes when YouTube changes something

## Where the APK lives

| | What's there | Used by |
|---|---|---|
| This site — `https://rajkumar30598.github.io/Adfree-tube-landing/AdFree-Tube.apk` | Only the newest version | Download buttons, the app's update banner (`updateUrl`) |
| [GitHub Releases](https://github.com/rajkumar30598/Adfree-tube-landing/releases) | Every version, never deleted | Archive, and the "Get it from GitHub" fallback link |

- **APKs are never committed to git.** The deploy downloads the newest one from Releases each time, so the repo stays small and the old APK disappears from the site automatically.
- **Cache busting:** the page links to `AdFree-Tube.apk?v=<latestVersion>`, so browsers don't reuse a cached older copy.
- **Why not link to Releases directly?** Release files are served from `release-assets.githubusercontent.com`, and one of its addresses is unreachable on some networks, so about 1 in 4 downloads stalled or failed. This site is served from different addresses.
- **In-app browsers** (Instagram, Facebook, Telegram…) often can't save APKs, so the page shows an "Open this page in Chrome" hint there.

## Releasing

New versions are published from the app repo with `npm run release -- <x.y.z> "notes"`. It creates the GitHub Release, then updates `remote-config.json` here. That push redeploys the site with the new APK in about a minute.

To redeploy by hand (for example if a deploy failed): Actions → **Deploy Pages** → Run workflow.
