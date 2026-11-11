# visaworkshop.github.io

Website of the **VISA Workshop — Virtual ISA for Rapidly Evolving Architectures**.

- Permanent entry point: **https://visaworkshop.github.io** (redirects to the current edition)
- Current edition: **https://visaworkshop.github.io/2026** — the 1st Workshop, co-located with [MICRO 2026](https://www.microarch.org/micro59/), Athens, Greece — **Saturday, Oct 31, 2026, 13:00–18:00 EET**
- Contact: visa.workshop.chairs@gmail.com

## Repository layout

```
.
├── index.html        # root redirect → current edition (edit on yearly rollover)
├── .nojekyll         # tells GitHub Pages to serve files as-is (no Jekyll build)
└── 2026/
    ├── index.html    # workshop home: hero, dates, keynotes, program, people, venue
    ├── cfp.html      # archived 2026 call for papers
    ├── visa-favicon.{svg,png} # browser tab icon
    └── papers/       # accepted paper PDFs for this edition
```

Each year's directory is **fully self-contained** (styles are embedded in each
page and edition assets stay in that directory). That keeps old editions frozen and browsable forever,
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

## 2026 site checklist

Search both files under `2026/` for `TODO`:

- [x] **Post-workshop archive** — remove submission controls from the site,
      mark the call as closed, and link to the accepted papers and program.
- [x] **Room** — Ypsilon III-IV at InterContinental Athenaeum Athens, listed in
      the October 27 agenda and confirmed against the MICRO workshop page.
- [x] **Workshop agenda** — published six invited talks and four paper presentations,
      with closing remarks and a coffee break.
- [x] **October 27 agenda** — add Jian Huang's talk title and the venue; list
      opening remarks without a speaker, as in the updated agenda.
- [x] **October 30 agenda** — remove opening remarks and start LIAO HENG's
      invited talk at 13:00; retain its 13:40 end time and all later sessions.
- [x] **Invited talk titles** — include Borivoje Nikolic's title from the final agenda.
- [x] **Accepted papers** — list six accepted papers, authors, and supplied affiliations
      in the homepage's `#papers` section.
- [x] **Paper presentations** — list the four scheduled talks with their titles,
      presenters, and links to the corresponding accepted papers.
- [x] **Paper PDFs** — archive all six papers under `2026/papers/` and link them from the homepage.
- [ ] **TPC affiliations** — add affiliations to the confirmed members and
      extend the list as invitations are accepted.

## Yearly rollover (e.g., 2027)

1. Create `2027/` and copy the previous edition's HTML pages and favicon files.
2. Update the new edition's dates, program, people, and paper list. Store its
   PDFs in `2027/papers/`, using `VISA2027-<order>-P<submission-id>-<first-author-surname>.pdf`.
   Use a two-digit list position, a three-digit (minimum) submission ID, and
   ASCII filenames under 50 characters. Link papers using edition-relative
   paths such as `papers/VISA2027-01-P055-Smith.pdf`.
3. In the **root** `index.html`, update the favicon links, canonical URL,
   redirects, and fallback link for the new edition.
4. Add a small "Past editions" link in the new edition's footer if desired.
   Old years stay untouched at `/2026/`, `/2027/`, …

## Custom domain (optional, later)

If the committee buys a domain (e.g., `visa-workshop.org`), add it under
**Settings → Pages → Custom domain**, create the DNS records GitHub shows you,
and add a `CNAME` file to the repo root. All `visaworkshop.github.io/…` URLs
will keep working via redirect.
