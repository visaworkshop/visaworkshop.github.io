# visaworkshop.github.io

Website of the **VISA Workshop — Virtual ISA for Rapidly Evolving Architectures**.

- Permanent entry point: **https://visaworkshop.github.io** (redirects to the current edition)
- Current edition: **https://visaworkshop.github.io/2026** — the 1st Workshop, co-located with [MICRO 2026](https://www.microarch.org/micro59/), Athens, Greece — **Saturday, Oct 31, 2026, 13:00–17:00 EET** (soft close 17:30)
- Contact: visa.workshop.chairs@gmail.com

## Repository layout

```
.
├── index.html        # root redirect → current edition (edit on yearly rollover)
├── .nojekyll         # tells GitHub Pages to serve files as-is (no Jekyll build)
└── 2026/
    ├── index.html    # workshop home: hero, dates, keynotes, program, people, venue
    └── cfp.html      # call for papers: scope, topics, submission, review
```

Each year's directory is **fully self-contained** (styles are embedded in each
page, no shared assets). That keeps old editions frozen and browsable forever,
even as the design evolves. The cost: `2026/index.html` and `2026/cfp.html`
duplicate one `<style>` block — if you change shared styles, change both files.

## Deploying

The org `visaworkshop` already exists. Remaining steps:

**1 — Create the repository**

In the org: *New repository* → name it exactly `visaworkshop.github.io` →
visibility **Public** (required for GitHub Pages on the free plan) → do **not**
initialize with a README → *Create repository*.

**2 — Push the files** (pick one path)

*Path A — web upload, no git needed:* on the empty-repo page click
"uploading an existing file", then drag in the **contents** of this folder —
`index.html`, `README.md`, `.nojekyll`, and the `2026` folder — so that
`index.html` sits at the **repo root** (not inside a `visaworkshop.github.io/`
subfolder). Commit to `main`. Note: `.nojekyll` is a hidden file — enable
"show hidden files" in your file manager, or add it afterwards via
*Add file → Create new file*, name `.nojekyll`, leave it empty, commit.

*Path B — git command line:*

```bash
cd visaworkshop.github.io          # the unzipped folder
git init -b main
git add -A                          # -A picks up .nojekyll too
git commit -m "VISA 2026 website"
git remote add origin https://github.com/visaworkshop/visaworkshop.github.io.git
git push -u origin main             # authenticate with a PAT or SSH key
```

**3 — Turn on Pages**

Repo → *Settings → Pages → Build and deployment* → Source:
*Deploy from a branch* → Branch `main`, folder `/ (root)` → *Save*.
The *Actions* tab will show a "pages build and deployment" run; when it's
green (1–2 min), https://visaworkshop.github.io is live and redirects
to `/2026/`.

**4 — Finishing touches**

- Repo front page → *About* (gear icon) → set Website to
  `https://visaworkshop.github.io/2026`.
- Org → *People*: invite the other chairs; give at least 2–3 people the
  **Owner** role so the site never depends on one account.
- Org → *Settings → Authentication security*: require two-factor
  authentication.

Local preview before pushing:

```bash
cd visaworkshop.github.io
python3 -m http.server 8000
# open http://localhost:8000
```

## Before the CFP goes wide — placeholder checklist

Search both files under `2026/` for `TODO`:

- [x] **HotCRP link** — wired to `https://visa2026.hotcrp.com/` in the home page,
      CFP submission controls, and both footers.
- [ ] **HotCRP activation** — once approved, change the two CFP button labels to
      "Submit a paper" and remove the pending-activation notes from both pages.
- [ ] **Room** — announced by MICRO closer to the date; update the Venue
      section on `index.html`.
- [ ] **Keynote titles & abstracts** — Heng Liao and Onur Mutlu cards on
      `index.html`.
- [ ] **Panelists** — the panel row in the program table.
- [ ] **TPC affiliations** — add affiliations to the confirmed members and
      extend the list as invitations are accepted.
- [ ] **Proceedings & presentation policy** — the CFP currently states
      non-archival + in-person presentation; confirm both with the committee
      and with MICRO (hybrid policy) before announcing.

## Yearly rollover (e.g., 2027)

1. `cp -r 2026 2027`
2. Update the content of `2027/` (dates, program, people, edition number).
3. In the **root** `index.html`, change the three occurrences of `2026/`
   to `2027/` (meta refresh, canonical link, JS redirect).
4. Add a small "Past editions" link in the new edition's footer if desired.
   Old years stay untouched at `/2026/`, `/2027/`, …

## Custom domain (optional, later)

If the committee buys a domain (e.g., `visa-workshop.org`), add it under
**Settings → Pages → Custom domain**, create the DNS records GitHub shows you,
and add a `CNAME` file to the repo root. All `visaworkshop.github.io/…` URLs
will keep working via redirect.
