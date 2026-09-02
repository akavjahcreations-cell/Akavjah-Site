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

Fix applied (this build): the homepage / was incorrectly tagged
<meta name="robots" content="noindex"> in an earlier build, which would
have told Google to exclude it from search entirely. That tag is now
removed from the homepage only; the three section-root redirect pages
(/support/madorbitdash/, /support/foolmeonce/, /privacy/) correctly KEEP
noindex, since they're pure JS-redirect stubs with no real content -
their language subpages (e.g. /support/madorbitdash/en/) are what should
be indexed, and they don't carry noindex.

Social share images (Open Graph):
- support/madorbitdash/og-madorbitdash.png and support/foolmeonce/og-foolmeonce.png
  are the real 1200x630 preview images shown when a link to either game's
  support page is shared on Discord/iMessage/Slack/social. Built from the
  actual App Store icons you provided. Wired via og:image + twitter:image
  meta tags on all 8 language versions of both games' support pages.
- The homepage has no og:image yet (no Akavjah Creations brand image exists
  yet) - add one later by dropping a 1200x630 PNG at the root and pointing
  H[lang]["og_image"] at it, same pattern as the two games.

Static section-root landing pages:
- /support/madorbitdash/, /support/foolmeonce/, and /privacy/ are no longer
  bare JS-redirect stubs with noindex - they're now real static pages
  (still auto-redirect visitors to their language via JS, but the HTML
  itself is indexable) so Google can list the section root as its own
  search result alongside the specific language pages.

Pricing note (Mad Orbit Dash):
- Current About-section copy says "Free to play" in all 8 languages, per
  owner confirmation that Apple approved a new free + 8-language version
  (superseding an earlier $0.99 listing). If a future App Store version
  changes pricing again, update MOD_ABOUT in generate.py accordingly -
  search for "about_p" under "MAD ORBIT DASH ABOUT".

Breadcrumb structured data:
- All 24 content pages (8 languages x MOD support / FMO support / privacy)
  now carry BreadcrumbList JSON-LD (Akavjah Creations > Support > [game]
  or Akavjah Creations > Privacy policy). This can make Google show a
  breadcrumb trail in search results instead of a raw URL. No visible
  on-page change.

Inline app icons + mailing address:
- Real App Store icons (from the files you provided) now appear inline
  next to the "About [game]" heading on both games' support pages, all
  8 languages - support/madorbitdash/icon-madorbitdash.png and
  support/foolmeonce/icon-foolmeonce.png.
- A mailing address block was added under the contact email on every
  page that has a contact card (homepage, both games' support pages,
  privacy policy - all 8 languages): Akavjah Creations, PO Box 220300,
  Chantilly, VA 20153, United States. "United States" was added by
  Claude for international clarity/deliverability since it wasn't in
  the address as given - remove it in generate.py's MAILING_ADDRESS
  constant if not wanted. The address itself is not translated (postal
  addresses conventionally aren't); only the label above it
  ("Mailing address" / "Adresse postale" / etc.) is localized per
  language, in the ADDR_LABEL dict.

Icon fix: the "About [game]" heading previously showed both the site's
decorative orb-dot bullet (used before every h2) and the real App Store
icon. The orb bullet is now suppressed on that specific heading only
(via the about-h2 CSS class) - the real icon is the only thing shown.
Every other section heading keeps its orb bullet as before.

Site navigation + brand logo (this build):
- Real clickable site navigation added: Home / Support / Privacy links now
  appear on every page (homepage, support hub, both games, privacy),
  all 8 languages. Previously these pages were only reachable by typing
  the direct URL.
- New generic Support hub at /support/{lang}/ - lists both games with
  their icons and links to each game's specific support page. This is
  what "Support" in the nav points to.
- Homepage: old in-page Story/Build Log/Mad Orbit Dash jump-nav removed
  in favor of the new site-wide nav; hero CTA buttons still jump to the
  same in-page sections as before.
- Official trademark logo (brand/logo-full.png, brand/logo-small.png)
  now used: large + centered in the homepage hero, small version in
  every page's header next to "Akavjah Creations", and again (46px,
  right-aligned) next to the contact info in every contact card.
- "Akavjah Creations" now carries a ™ superscript (header wordmark +
  footer copyright line, every page) since the trademark is pending,
  not yet registered - do NOT change this to ® until USPTO actually
  grants registration; using ® before that is legally improper.
- Homepage now has a real Open Graph share image (brand/og-homepage.png)
  and the whole site has a proper favicon (brand/favicon.ico,
  favicon-32.png, favicon-512.png, apple-touch-icon.png) - both were
  previously blocked on having no brand asset.

Fixes in this build:
- sitemap.xml was missing the new /support/{lang}/ hub pages (added when
  the hub was built, but the sitemap generator wasn't updated at the
  time). Fixed: 36 -> 45 URLs now listed.
- Added a branded 404.html at the repo root. GitHub Pages serves this
  automatically for any broken/mistyped URL. Detects browser language
  client-side (same pattern as the other redirect stubs) and links to
  Home and Support in the right language.

Accessibility pass (this build):
- Verified: color contrast on every text/bg pairing clears WCAG AA with
  real margin (7:1-15:1 vs 4.5:1 minimum); alt text present on every
  image, scanned across all pages; lang attributes correct everywhere.
- Fixed: decorative gameplay videos now carry aria-hidden="true" - the
  parent link already has a proper aria-label describing the video, so
  screen readers now skip the unlabeled <video> element cleanly instead
  of announcing an ambiguous media control.
- Removed: the old animated-SVG placeholder logo (unused since the real
  trademark logo replaced it everywhere) and its now-orphaned CSS.

Dead code sweep (this build):
- Removed .backlink CSS (unused since the old "← Back to site" link was
  replaced by the Home/Support/Privacy nav bar).
- Removed the 16 now-unused "back" translation strings (one per language,
  x2 for MOD support + privacy content) that fed that old link, plus the
  dead threading that carried them through to page_shell() without ever
  being rendered.
- Verified via automated scan: zero unused CSS classes remain anywhere
  in the generated site.
