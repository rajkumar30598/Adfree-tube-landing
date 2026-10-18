# AdFree Tube — website

Landing page for AdFree Tube, served with GitHub Pages:
**https://rajkumar30598.github.io/Adfree-tube-landing/**

- `index.html` — the page (no build step). It reads `remote-config.json` to show the version and size.
- `download/AdFree-Tube-<version>.apk` + `versions.json` — every version, listed in the page's "All versions" section.
- `download/AdFree-Tube.apk` — the newest APK, served at `https://rajkumar30598.github.io/Adfree-tube-landing/download/AdFree-Tube.apk`.
- `remote-config.json` — read by the app at start-up. Edit it here to push fixes or messages to every user without an update:
  - `latestVersion` / `latestNotes` / `apkSize` / `releasedAt` / `updateUrl` — shows an "update available" banner to older versions
  - `minVersion` — forces an "update needed" banner
  - `notice` — a one-off message (`id`, `title`, `message`, optional `url`/`button`)
  - `clients`, `trendingQueries`, `pipedInstances` — hotfixes when YouTube changes something

New versions are published from the app repo with `npm run release`.
