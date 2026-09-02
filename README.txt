Akavjah Creations — akavjah.com
================================
Full localized site: homepage, both games' support pages, privacy
policy, and a generic support hub — each in 8 languages (en fr it es
de zh ja ko) — plus sitemap, robots.txt, a branded 404 page, and
favicon/social-share assets.

DEPLOY
------
Delete everything currently in the GitHub Pages repo root, then copy
every file/folder from inside this unzipped folder (not the folder
itself) into the now-empty repo root. Commit and push. GitHub Pages
rebuilds automatically within a few minutes.

SITE STRUCTURE
--------------
/                              redirect stub -> /{lang}/ by browser language
/{lang}/                       homepage (8 languages)
/support/                      redirect stub -> /support/{lang}/
/support/{lang}/               support hub: pick Mad Orbit Dash or Fool Me Once
/support/madorbitdash/         redirect stub -> .../{lang}/ (static, indexable)
/support/madorbitdash/{lang}/  Mad Orbit Dash support page + About section
/support/foolmeonce/           redirect stub -> .../{lang}/ (static, indexable)
/support/foolmeonce/{lang}/    Fool Me Once support page + About section
/privacy/                      redirect stub -> /privacy/{lang}/ (static, indexable)
/privacy/{lang}/               privacy policy
/404.html                      branded not-found page, GitHub Pages auto-serves this
/brand/                        logo, favicons, homepage OG share image
/sitemap.xml, /robots.txt      SEO — submitted to Google Search Console

All redirect stubs use client-side JS to detect the visitor's browser
language and bounce to the matching /{lang}/ path, falling back to
English. The three section-root stubs (support/madorbitdash/,
support/foolmeonce/, privacy/) are NOT pure JS-redirect-only — their
raw HTML is real, indexable content (no noindex) so Google can list
the section root itself, not just the language subpages.

NAVIGATION
----------
Every page has a header with the trademark logo + wordmark (links
home) and a Home / Support / Privacy nav bar — added so the site is
click-navigable, not just reachable by typing exact URLs. The Support
hub is the "which game do you need help with" picker page.

BRANDING
--------
Real trademark logo (Akavjah Creations crest) used: small version in
every page header, large centered version in the homepage hero, and a
128px version next to the contact card on every page that has one
(homepage, both games, privacy). "Akavjah Creations" carries a TM
superscript (trademark pending, not yet registered — do NOT change to
(R) until USPTO actually grants registration).

GAME SUPPORT PAGES — About sections
------------------------------------
Both games' support pages open with an About section: description,
looping gameplay video, and an official "Download on the App Store"
badge, all linking to the App Store listing.
- Mad Orbit Dash: genuinely localized App Store listing, so each
  language gets ITS OWN gameplay clip (from Apple's own per-language
  preview exports) and the matching localized Apple badge.
- Fool Me Once: app is English-only, so every language shares the
  same clip, same link, and the English-locale badge; only the
  description text is translated. Update this if the app is ever
  localized.
Also: real App Store icons (provided by the owner) shown inline next
to each "About [game]" heading.

CONTACT INFO
------------
Every contact card shows: email (akavjahcreations@gmail.com) + mailing
address (Akavjah Creations, PO Box 220300, Chantilly, VA 20153, United
States — "United States" added by Claude for international clarity,
not originally given) + the 128px trademark logo.

TRANSLATION STANDARD
---------------------
Natural native idiom, not literal word-for-word translation — but
never invent wordplay/puns where the English source is plain. Keep in
English everywhere: game titles, GameEngine.swift, sfx_tap.wav, "vibe
coding", "build target", HUD labels (BEST/SCORE/PREV), and — for Fool
Me Once specifically — the quoted in-game UI strings ("Restore
Purchase", "Read more", "Full Game", "Endless") since that app isn't
localized yet.

SEO
---
hreflang (+ x-default) on every page, canonical URLs, unique
title/description per language, JSON-LD structured data
(SoftwareApplication + FAQPage + BreadcrumbList on relevant pages),
Open Graph + Twitter Card images (per-game images built from the real
app icons; homepage image built from the trademark logo), sitemap.xml
covering all 45 real URLs, robots.txt pointing at it.

ACCESSIBILITY
-------------
Verified: color contrast on every text/background pairing clears WCAG
AA with real margin (7:1-15:1 measured, vs 4.5:1 minimum); alt text
present on every image; correct lang attribute on every page.
Decorative gameplay videos carry aria-hidden="true" since the
surrounding link already has a proper aria-label describing them.

REGENERATING
------------
The whole site is built by generate.py from per-language content
dictionaries (S = game support content, P = privacy, H = homepage,
F = Fool Me Once support, SUPPORT_HUB = hub page). Edit the relevant
dict, run `python3 generate.py`, and the entire output tree in
akavjah-localized/ is rebuilt from scratch. Do not hand-edit the
generated HTML directly — it will be overwritten on the next run.
