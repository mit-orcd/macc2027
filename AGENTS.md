# AGENTS.md - maintainer guide for the Project MACC 2027 site

This file gives an AI agent (or a new human maintainer) the context needed to
keep this site accurate and consistent. Read it before editing anything.

## What this repository is

The public website for **Project MACC 2027 - an MIT Agentic Coding
Challenge**, a multi-month contest (October 2026 - January 2027) run by the
MIT Office of Research Computing and Data (ORCD) that awards prizes for the
best uses of agentic coding to advance research and education missions at
MIT.

The site is a static, dependency-free set of pages: plain HTML plus one CSS
file. There is no build step, no JavaScript, no framework, and no package
manager. Edit the HTML/CSS directly; what is in `docs/` is exactly what gets
served.

## Layout

| Path | Purpose |
|---|---|
| `docs/index.html` | Contest overview: what it is, areas, technology stances, rules in brief, what ORCD provides, timeline |
| `docs/prizes.html` | $5,000 Grand Prize, seven $2,000 Area Prizes, judging criteria, vendor prizes |
| `docs/signup.html` | Team sign-up page linking to a Google Form |
| `docs/404.html` | Not-found page; uses root-absolute paths (`/assets/...`), unlike the other pages which use relative paths |
| `docs/assets/style.css` | All styling for every page |
| `docs/assets/img/logo-orcd.svg` | ORCD logo lockup, downloaded from orcd.mit.edu |
| `docs/.nojekyll` | Tells GitHub Pages to serve files as-is (no Jekyll) |
| `docs/README.md` | Deployment and DNS instructions |

## Hosting

Published with GitHub Pages from the `docs/` folder on `main`. Pushing to
`main` deploys the site.

Custom domain status: a `docs/CNAME` file for `macc27.mit.edu` was originally
committed and later deliberately deleted on GitHub (commit "Delete CNAME").
Do not re-add a CNAME file unless the maintainer says the custom domain is
being set up. The intended DNS arrangement (macc27.mit.edu as primary,
macc.mit.edu redirecting to it) is documented in `docs/README.md`, including
the caveat that a bare DNS ALIAS for macc.mit.edu will not work with GitHub
Pages - an HTTP redirect is required.

## Known open items

- **Google Form URL is a placeholder.** `docs/signup.html` links to
  `https://forms.gle/REPLACE-WITH-FORM-ID`. That is deliberately the only
  place on the site where the form URL appears. When the real form exists,
  replace it there and nowhere else.
- The custom domain is not currently configured (see Hosting above), so the
  site serves from the default github.io URL until that changes.

## Editorial rules (important - these came from the maintainer)

1. **No em dashes.** The maintainer explicitly dislikes them. Use a spaced
   hyphen (" - ") or reword. En dashes are acceptable in ranges
   ("October 2026 – January 2027") and in "human–machine collaboration".
2. **Naming.** The project is "Project MACC 2027". The subtitle is
   "**An** MIT Agentic Coding Challenge" - "An", not "The".
3. **Area names** use the @MIT style: Science@MIT, Engineering@MIT,
   Architecture and Planning@MIT, Humanities, Arts, and Social Sciences@MIT,
   Management@MIT, Computing@MIT, Education@MIT.
4. **The open-source eligibility note is a footnote.** "For legal reasons,
   participants who choose not to or are unable to open-source their work
   will not be eligible for prizes." appears as footnote 1 (superscript
   `fn-ref` marker, `.footnotes` block above the footer) on both
   `index.html` and `signup.html`. Keep that pattern if the text moves.
5. **Footer** on every page: ORCD attribution, contact
   `orcd-help@mit.edu`, and an "Accessibility" link to
   https://accessibility.mit.edu/. Do not reintroduce personal email
   addresses.
6. The maintainer supplies most wording changes verbatim. Apply them
   faithfully; it is acceptable to fix obvious typos and grammar slips, but
   say so explicitly when reporting back.

## Consistency traps

Several pieces of copy are intentionally duplicated across pages and must be
kept in sync when one instance changes:

- The **footer** markup is identical on all four pages (404.html differs
  only in using absolute paths).
- The **header/nav** markup is identical on all four pages except for which
  link carries `class="current"` (and absolute paths on 404.html).
- The **technology stance list** (open-weight models, open-source harnesses,
  commercial models and agents, bring-your-own scaffolds, robust research
  software engineering, or deterministic, verifiable modeling) appears on
  both `index.html` and `signup.html`.
- The contest goal phrase ("to advance research and education missions at
  MIT") appears in the hero, the opening paragraph, and the meta description
  of `index.html`, and on the Grand Prize card in `prizes.html`.

When replacing a phrase site-wide, remember the HTML is hard-wrapped at
roughly 80 columns: a target phrase may be split across a line break, so a
single-line grep/sed can miss instances. Grep for a distinctive fragment of
the phrase to confirm you caught them all.

## Design system

Defined entirely in `docs/assets/style.css` via CSS custom properties:

- `--orcd-teal: #36ab9c` - the logo teal, sampled from orcd.mit.edu; used
  for decorative elements.
- `--orcd-band: #4da59e` - the nav band background, matching the ORCD site;
  dark text goes on top of it.
- `--accent: #1f756b` / `--accent-dark: #175c54` - darkened teal for links,
  headings, buttons, and prize amounts. This is deliberate: the brighter
  logo teal fails WCAG contrast on white for small text, so do not swap
  `--accent` for `--orcd-teal` on text.
- Header pattern mirrors orcd.mit.edu: white masthead with the ORCD logo
  (linking to orcd.mit.edu) and the MACC wordmark, then a full-width teal
  nav band with bold dark links and a white "Sign Up" pill.

## Key content facts (as currently published)

- **Grand Prize:** one, $5,000, awarded across all areas.
- **Area Prizes:** seven, $2,000 each, aligned to MIT's five schools plus
  the Schwarzman College of Computing and MIT Education (residential
  teaching and Open Learning).
- **Vendor prizes:** hardware (NVIDIA DGX Spark, AMD Strix Halo, Dell Pro
  Max with GB10 systems, and more) and cloud credits, drawn from
  cross-cutting categories; a "noble failure" prize may also be awarded.
- **Prizes are split evenly** among team members; teams of any size,
  including one, are welcome. Teams must include at least one member of the
  MIT community.
- **Judging:** finalists are judged on an open-source piece of software, a
  short write-up, and a live presentation at the January showcase. Three
  headline criteria: contribution to the elected area; technical capability,
  innovation, and originality; robustness and reproducibility.
- **Timeline:** Oct 2026 launch and onboarding; Nov-Dec 2026 build period;
  early Jan 2027 IAP sprint; late Jan 2027 submissions close, judging,
  showcase and awards; Feb 2027 public results report.
- **Infrastructure:** ORCD operates two reference setups (sandboxed, pinned
  execution); contestants may use any hardware they like, and no prize
  requires the reference setups.

If a factual change is requested (prize amounts, dates, areas), update every
page where the fact appears - check `index.html`, `prizes.html`, and
`signup.html`, including `<meta name="description">` tags.

## Workflow conventions

- Work on `main`; there is no branch/PR ceremony for routine copy edits
  unless the maintainer asks for it.
- **Do not commit or push without being asked.** The maintainer reviews
  changes and says "commit" / "push" explicitly, usually per batch of edits.
- Commit messages: an informative subject line and a short body describing
  the change, ending with the line `Assisted by AI.` Do not add
  `Co-Authored-By:` trailers for the AI - the AI assists with writing the
  pages, and claiming authorship in the traditional sense would be
  misleading. E.g.:

  ```
  Footer: add MIT Accessibility link, switch contact to orcd-help@mit.edu

  Every page footer now links to https://accessibility.mit.edu/ and uses
  orcd-help@mit.edu as the contact address.

  Assisted by AI.
  ```

- If a push is rejected, fetch and inspect what changed on the remote before
  integrating - changes are sometimes made directly on GitHub (the CNAME
  deletion happened that way). Rebase local commits on top and preserve the
  remote's intent.

## Verifying changes

No test suite; verify visually and by link check:

- Serve locally: `python3 -m http.server` from inside `docs/`, then browse
  http://localhost:8000/.
- Quick link audit: `grep -ho 'href="[^"]*"' docs/*.html | sort -u` and
  confirm every relative target exists.
- Headless screenshots (macOS):
  `"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless
  --disable-gpu --screenshot=/tmp/out.png --window-size=1200,1400
  "file:///path/to/docs/index.html"`.
- After pushing, GitHub Pages redeploys automatically within a few minutes.
