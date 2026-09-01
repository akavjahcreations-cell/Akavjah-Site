Akavjah Creations — localized support & privacy pages
=====================================================

Copy the folders AND the root index.html into the ROOT of your GitHub Pages repo,
preserving the structure:

  /index.html                           <- homepage: auto-redirects by browser language
  /{en,fr,it,es,de,zh,ja,ko}/index.html <- localized homepages
  /support/madorbitdash/index.html      <- auto-redirects by browser language
  /support/madorbitdash/{en,fr,it,es,de,zh,ja,ko}/index.html
  /privacy/index.html                   <- auto-redirects by browser language
  /privacy/{en,fr,it,es,de,zh,ja,ko}/index.html

Notes:
- Redirect logic walks the visitor's full browser-language list and
  falls back to English. No JS -> meta refresh to /en/.
- Every localized page carries hreflang tags (zh uses zh-Hans) plus
  x-default -> English, a canonical URL, and a language switcher footer.
- App Store Connect: keep the support URL as
  https://www.akavjah.com/support/madorbitdash/ - the redirect does the rest.
  Optionally set per-locale marketing URLs (e.g. /support/madorbitdash/ja/)
  in each localization's metadata.
- If your existing pages have site-wide styling you prefer, the content of
  each page is plain semantic HTML inside <main> - easy to restyle.

Homepage note:
- The root /index.html REPLACES your current homepage with the language
  redirect. Your existing homepage content lives on, translated, at /en/ etc.
- In-page anchors (#story #log #game) work within each language version.
- The mock HUD labels (BEST / SCORE / PREV) are left in English on purpose,
  to match the actual in-game interface.
Fool Me Once:
- /support/foolmeonce/ follows the same pattern: root index.html redirects,
  /{lang}/ holds the localized pages (5 FAQs incl. purchase restore).
- Fool Me Once is currently English-only, so quoted in-game strings
  ("Restore Purchase", "Read more", "Full Game", "Endless") are kept in
  English on all localized pages so players can find them on screen.
  If the app gets localized later, translate those quoted strings to match.
- Every FMO support page (all 8 languages) now opens with an "About"
  section: translated blurb + looping gameplay clip + App Store badge,
  both linking to the listing. Since FMO has no localized App Store page,
  every language uses the SAME English-locale Apple badge image, the same
  gameplay-foolmeonce.mp4, and the same store link — only the blurb text
  is translated.

Mad Orbit Dash — per-language gameplay videos:
- Each MOD support page now opens with an "About" section like Fool Me
  Once's, but MOD DOES have a localized App Store listing, so each
  language gets its OWN gameplay clip (from Apple's own per-language App
  Store preview exports) and Apple's per-language "Download on the App
  Store" badge:
    en -> gameplay-madorbitdash-en.mp4  (badge: en-us)
    fr -> gameplay-madorbitdash-fr.mp4  (badge: fr-fr)
    it -> gameplay-madorbitdash-it.mp4  (badge: it-it)
    es -> gameplay-madorbitdash-es.mp4  (badge: es-es)
    de -> gameplay-madorbitdash-de.mp4  (badge: de-de)
    zh -> gameplay-madorbitdash-zh.mp4  (badge: zh-cn)
    ja -> gameplay-madorbitdash-ja.mp4  (badge: ja-jp)
    ko -> gameplay-madorbitdash-ko.mp4  (badge: ko-kr)
  Videos live at support/madorbitdash/ (same level as the language folders).

THIS IS A FULL REPLACEMENT DROP:
- Delete everything in your GitHub Pages repo root, then copy in the
  entire contents of this folder (not the folder itself) in its place.
- Commit and push. Give Pages a couple of minutes, then hard-refresh.
