# Project MACC 2027 - stand-alone website

A self-contained static site for **Project MACC 2027 - an MIT Agentic Coding
Challenge**, suitable for hosting on GitHub Pages at the address
`macc27.mit.edu`, with `macc.mit.edu` aliased to it. No build step, no
dependencies: plain HTML and one CSS file.

## Contents

| File | Purpose |
|---|---|
| `index.html` | The contest: what it is, how it's organized, rules in brief, timeline |
| `prizes.html` | The $5,000 Grand Prize and the seven $2,000 Area Prizes |
| `signup.html` | Team sign-up page linking to the Google Form |
| `assets/style.css` | All styling |
| `assets/img/logo-orcd.svg` | ORCD logo lockup, downloaded from orcd.mit.edu |
| `404.html` | Not-found page (uses absolute paths; assumes the site is served at the domain root) |
| `CNAME` | Custom-domain marker for GitHub Pages (`macc27.mit.edu`) |
| `.nojekyll` | Tells GitHub Pages to serve files as-is, without Jekyll processing |

## Before going live

**Set the Google Form URL.** Edit `signup.html` and replace the placeholder
`https://forms.gle/REPLACE-WITH-FORM-ID` with the real Google Form link. That
is the only place on the site where the form URL appears.

## Hosting on GitHub Pages

1. Push the contents of this folder to the **root** of a GitHub repository
   (or copy it into a `docs/` folder of an existing repo).
2. In the repo: **Settings → Pages**, set the source to the branch (and
   `/` root or `/docs` as appropriate).
3. Under **Custom domain**, enter `macc27.mit.edu` (the `CNAME` file in this
   folder keeps that setting from being lost on redeploys). Enable
   **Enforce HTTPS** once the certificate is issued.

## DNS setup

Ask MIT IS&T for two records:

1. **Primary domain - CNAME record:**
   `macc27.mit.edu → <org-or-user>.github.io`. GitHub then serves the site
   directly at `https://macc27.mit.edu/` with a proper certificate.
2. **Alias - ALIAS record:** `macc.mit.edu → macc27.mit.edu`, so the short
   address resolves to the same place.

**Caveat on the ALIAS:** DNS aliasing makes `macc.mit.edu` *resolve* to the
same GitHub servers, but GitHub Pages only answers for the custom domain
configured in the repo (`macc27.mit.edu`). Requests arriving with a
`macc.mit.edu` Host header will get GitHub's 404 page, and HTTPS will show a
certificate warning. If visitors typing `macc.mit.edu` should land on the
site, ask IS&T for an **HTTP redirect** from `macc.mit.edu` to
`https://macc27.mit.edu/` instead of (or in addition to) the ALIAS record -
that is the arrangement that actually works end to end.

## Previewing locally

Open `index.html` directly in a browser, or run a local server from this
folder:

```sh
python3 -m http.server 8000
```

then visit <http://localhost:8000/>.
