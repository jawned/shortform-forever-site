# Privacy Policy — Shortform Forever

_Last updated: 2026-07-10_

Shortform Forever is a local archiver for your own TikTok account (liked
videos, favorited videos, and new uploads from creators you follow). It has
**no server component operated by the developer, no analytics, and no
telemetry.** Everything the extension touches stays on your own machine,
between your browser and a companion program (the "local service") that also
runs on your machine.

## What the extension does

The Shortform Forever browser extension is a thin bridge between
`tiktok.com` (where it reads your account's liked/favorited/following lists,
authenticated as you) and the local service running on your own computer
(where those lists get archived to a local database). It does not talk to
any server other than `tiktok.com` and `127.0.0.1` (your own machine).

## Permissions, and why each one is needed

- **`cookies` on `tiktok.com`** — used to read your session cookie so the
  local service can make authenticated requests to TikTok's API on your
  behalf (for parts of the sync TikTok's public API doesn't expose). The
  cookie value is sent **only** to the local service on `127.0.0.1`, over a
  connection authenticated with a token the service itself generates and
  shares only with this extension. It is never sent anywhere else, never
  logged, and never leaves your machine.
- **`nativeMessaging`** — lets the extension start the local companion
  program (if it isn't already running) and retrieve the auth token
  mentioned above from it. Nothing else is exchanged over this channel.
- **`host_permissions`: `http://127.0.0.1/*`** — the local service the
  extension talks to. Requests to this host carry the shared auth token; the
  service refuses requests that don't present it.
- **`host_permissions`: `*://*.tiktok.com/*`** — needed to read your
  liked/favorited/following lists from TikTok's pages while you're logged in,
  so they can be archived locally.
- **`tabs`** — used to open/manage the small background tab the extension
  uses to drive TikTok's list pages during a sync, and to detect when you're
  looking at a TikTok page.
- **`scripting`** — used to inject the sync logic into TikTok pages (the
  content scripts declared in the manifest).
- **`storage`** — used to remember non-sensitive local state (the archive
  service's cached URL/port, sync progress) between browser sessions. Stored
  only in your browser's local extension storage; never synced to a Google
  account or any remote service.

## What we don't do

- No remote servers of any kind receive your data. The only network
  destinations are `tiktok.com` (to read your own lists) and `127.0.0.1`
  (your own machine).
- No analytics or telemetry, from the extension or the local service.
- No selling, sharing, or transmitting of your data to any third party —
  there is no third party in this picture.
- No remotely fetched or `eval`'d code — everything the extension runs ships
  in the reviewed package.

## Data retention and control

All archived data (videos, metadata, thumbnails) lives in a local SQLite
database and file structure on your own computer, under your control. Delete
it any time by deleting the local archive folder. Uninstalling the extension
stops the sync; it does not delete anything already archived, since that data
was never in the extension's possession — only your own machine's.

## Single purpose

Shortform Forever's single purpose is: archive your own TikTok account
(liked, favorited, and followed-creator videos) to a local database and
folder you control.

## Contact

This is an independent, non-commercial hobby project. Questions or concerns
about this policy: open an issue at the project's GitHub repository.
