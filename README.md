# rohy-content

Imaging and slide content for [rohy](https://github.com/mohsaqr/rohySimulator),
published as release assets. **This repository holds no source** — only tagged
releases carrying the archives a deployment installs.

## Installing it

From a rohy checkout:

```bash
npm run setup:content
```

That downloads the archives for this release, verifies them by SHA-256, and
installs them under `server/plugin-content/`, which rohy serves from its own
disk. One transfer per deployment rather than one per tile per learner, and
nothing depends on this repository being reachable afterwards. Re-running it is
a no-op.

If your network cannot reach GitHub — an air-gapped hospital, a restricted
site — download the assets any way you like and point at them:

```bash
npm run setup:content -- --from /media/usb/rohy-content
npm run setup:content -- --only pathology          # slides without the imaging
```

The installer trusts the checksum recorded in rohy's
`scripts/content-sources.json`, not the place the bytes came from, so any
transport works and a truncated or substituted file is refused before anything
is installed.

## What is in a release

| asset | contents |
|---|---|
| `rohy-content-pacs-<version>.tar.gz` | the imaging archive — DICOM series and thumbnails |
| `rohy-content-pathology-<version>.tar.gz` | Deep Zoom slide pyramids and previews |

Each archive carries a `content.json` describing itself (file count, bytes, a
SHA-256 per file) and a `catalog.json` listing what a case author may reach.

## Licensing

Every entry is redistributable and says so in its own provenance record: CC0
and public-domain material outright, CC BY and CC BY-SA material while the
attribution notice ships with it. Those notices are inside the archives, in
`catalog.json`, and rohy displays them.

Nothing here was included because it was convenient to include. An entry whose
licence was never established does not ship, which is why three whole-slide
images in the source library are absent from these archives.

Sources include The Cancer Imaging Archive, the Cardiac Atlas Project
(Sunnybrook Cardiac Data, CC0), the National Library of Medicine's Visible
Human Project, and openly licensed clinical figures and loops from the
cardiology and pathology literature via Wikimedia Commons.

## Provenance

Built from the archives in `Radoyon` and `Pathoyon` with `npm run pack:content`.
The archives themselves are not committed anywhere: they are reproducible from
those repositories' own ingest manifests, which record for every entry where it
came from, under what licence, and who checked.
