# GUARDIAN-NIDS — project page

A single-file, zero-dependency project page for **GUARDIAN-NIDS**: a six-benchmark
evaluation of classical, neural and ensemble models for network intrusion detection,
with a from-scratch NumPy Random Forest deployment path.

Everything — layout, charts, data — lives in `index.html`. No build step, no
framework, no npm install. The only external request is the Google Fonts
stylesheet; the page degrades gracefully to system fonts without it.

```
.
├── index.html      the whole site (~130 KB)
├── vercel.json     clean URLs + security headers
└── README.md       this file
```

---

## Deploy to Vercel

### Option A — Vercel CLI (fastest)

```bash
npm i -g vercel      # once
cd guardian-nids-site
vercel               # preview deployment, follow the prompts
vercel --prod        # promote to production
```

When asked to *"link to an existing project"*, choose **no** and accept the
defaults. Framework preset: **Other**. Build command: leave empty. Output
directory: leave empty (Vercel serves the repo root).

### Option B — GitHub → Vercel (recommended for ongoing edits)

```bash
cd guardian-nids-site
git init
git add .
git commit -m "GUARDIAN-NIDS project page"
git branch -M main
git remote add origin https://github.com/<you>/guardian-nids-site.git
git push -u origin main
```

Then at [vercel.com/new](https://vercel.com/new): **Import Git Repository** →
select the repo → Framework Preset **Other** → **Deploy**. Every push to `main`
redeploys automatically, and every pull request gets its own preview URL.

### Option C — drag and drop

Go to [vercel.com/new](https://vercel.com/new), drop the whole folder onto the
upload area, and deploy. Fine for a one-off; use A or B if you plan to iterate.

---

## Custom domain

Vercel dashboard → your project → **Settings → Domains** → add
e.g. `guardian-nids.yourdomain.com`, then add the CNAME record Vercel shows you
at your DNS provider. TLS is issued automatically.

---

## Editing

### Content
All prose is plain HTML inside `index.html`, grouped by section
(`#overview`, `#architecture`, `#benchmarks`, `#method`, `#models`,
`#results`, `#scratch`, `#robustness`, `#engineering`).

### Data
Every chart and table is driven by the constants at the top of the `<script>`
block, each annotated with the report table it came from:

| Constant | Source |
|---|---|
| `STRATEGIES` | column order for every matrix — keep in sync with `F1` |
| `DATASETS` | Table 2 — row counts, encoded feature dimensions, split notes |
| `F1` | Table 9 — standard-test macro-F1, 12 cases × 10 strategies |
| `RANK` | Table 11 — descriptive ranking incl. the scratch forest |
| `VALRANK` | Table 5 — validation ranking of the seven standalone algorithms |
| `BEST` | Table 8 — best strategy per dataset–task case |
| `GAP` | Table 14 — binary vs multi-class reduction |
| `INFLATE` | Table 15 — ten largest accuracy / macro-F1 gaps |
| `RFCMP` | Table 13 — library vs scratch Random Forest, case level |
| `STRESS` | Table 16 — KDDTest+ vs KDDTest-21 |
| `EFF` | Table 17 — performance and resource summary |
| `MODELINFO` | Tables 3 & 4 — model roles and reference configurations |
| `CODE` | the four syntax-highlighted code panes |

Change a number in one of those arrays and every chart, table and tooltip that
uses it updates — there is no duplicated data in the markup.

### Theme
Colours, spacing and type live in the `:root` custom properties at the top of
the `<style>` block. `--teal` is the accent used across charts, links and
highlights; `--rose` marks the scratch implementation; `--amber` and `--violet`
mark the multi-class and ensemble series.

### Preview locally

```bash
python3 -m http.server 8000     # then open http://localhost:8000
```

Or just open `index.html` in a browser — it works from `file://` too.

---

## Reusing this as a template for other projects

The page is deliberately structured so a second project can reuse it:
keep the `<style>` block and the section shell, replace the data constants and
the prose. The chart helpers (`drawHeatmap`, `drawLeaderboard`, `groupedBars`,
the log-scale scatter, `animateBars`, the tooltip) are generic and take plain
arrays.

---

## Notes

- Every figure on the page is transcribed from the MSSD 51.506 Project 2 final
  report, which in turn is generated from `results_finalWithRF_Scratch.csv`.
- The repository link points at `github.com/alvin21mfmlai/GUARDIAN-NIDS`, which
  is currently private — update or remove the three occurrences in `index.html`
  if that changes.
- No analytics, no cookies, no tracking, no browser storage.
