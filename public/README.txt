Enkareflow website - static hosting package
=============================================

Contents (upload everything, keeping the folder structure):
  index.html     Home
  services.html  Services
  about.html     About
  contact.html   Contact
  privacy.html   Privacy Policy
  terms.html     Terms of Use
  img/           Social-preview images (og:image). Keep at site root.
  _headers       Security headers (Cloudflare Pages / Netlify read this
                 automatically; other hosts ignore it harmlessly)
  robots.txt     Allows all crawlers, points to the sitemap
  sitemap.xml    The six page URLs for search engines

Deploying to Cloudflare Pages (recommended, free):
  1. dash.cloudflare.com -> Workers & Pages -> Create -> Pages
     -> Upload assets ("Direct Upload").
  2. Drag this whole folder in. Every later update is the same drag-and-drop;
     each upload becomes a new deployment you can roll back.
  3. Add your custom domain (enkareflow.com) under the project's
     Custom domains tab. HTTPS is automatic.
  The _headers file applies the security headers automatically. Do NOT add a
  Content-Security-Policy (see below).

SEO / social metadata:
  Title, description, canonical, Open Graph, Twitter tags and JSON-LD
  structured data (business info on Home, FAQ on Contact) are in each file's
  static <head>, readable without JavaScript. og:image URLs point to
  https://enkareflow.com/img/... so the img/ folder must be deployed.

Editing pages WITHOUT Claude:
  Each page is one self-contained HTML file. All visible text exists inside
  it as plain text, so small copy changes are safe with any text editor
  (VS Code, Notepad++, even Notepad):
    1. Open the file, e.g. contact.html.
    2. Ctrl+F for the exact sentence you want to change; it appears inside a
       long quoted block near the bottom of the file.
    3. Edit the words only. Do not touch anything that looks like
       \" or \n or <span ...> around them; those are code.
    4. If the same text also appears in the <head> (title, description,
       JSON-LD), update it there too.
    5. Save, re-upload the file to Cloudflare Pages, done.
  Rules of thumb:
    - Text and phone/email swaps: safe by hand.
      (The WhatsApp number appears as 2548003569 in links and the form code,
       shown as +254-800-FLOW in visible text; replace every occurrence
       with your real digits-only number.)
    - Swapping a photo, adding a section, layout changes: not hand-editable;
      these need the source project (or any web developer working from it).
  Keep a copy of the original file before editing so you can roll back.

Contact form:
  The "Send inquiry" button opens the visitor's WhatsApp (or email)
  pre-filled to the business number. No server is needed and there is
  nothing for bots to submit to, so form spam is not possible.
  BEFORE LAUNCH: replace the +254-800-FLOW display number and its digits-only
  form/link value (currently 2548003569) with the real number.
  WhatsApp links need digits only (e.g. wa.me/2547XXXXXXXX).

Security notes:
  Do NOT add a restrictive Content-Security-Policy. Each page is a
  self-contained bundle that runs inline scripts and loads its own inlined
  assets; a strict CSP will blank the site. Leave CSP unset, or use only:
    Content-Security-Policy: frame-ancestors 'self'
  HTTP-to-HTTPS redirects are handled by Cloudflare automatically.
