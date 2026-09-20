# RedLoop-Browser — Learn & practise AI red teaming across the Agile lifecycle with A4SRAI

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)

**RedLoop-Browser** is the browser build of **RedLoop**: a self-guided, fully offline learning tool
that teaches the **Agile 4 Secure Responsible AI (A4SRAI)** framework, lets you practise AI red
teaming safely, structure your findings across the lifecycle, and check your understanding — ending
with a downloadable red-team report and a completion certificate.

It is a complete, feature-for-feature port of the Streamlit application to plain HTML, CSS and
JavaScript, so it can be hosted on **GitHub Pages** (or any static host) with **no server, no build
step, no Python and no installation**. Open the page and it works.

It is designed both as a standalone learning app for anyone starting to build AI systems, and as a
facilitator tool for workshops. It runs **fully offline**: no API keys, no internet calls, no
accounts, no telemetry. Nothing you type ever leaves your browser.

---

## Live demo

Once deployed (see [Deploying to GitHub Pages](#1-deploying-to-github-pages)), your app is at:

```
https://<your-username>.github.io/<your-repo>/
```

---

## What's inside

RedLoop-Browser is organised as a learner journey (Connections → Concepts → Concrete Practice →
Conclusions). Use the left sidebar to move between sections:

1. **Home** — onboarding, the A4SRAI diagram, your learning path and progress.
2. **Learn A4SRAI** — an interactive walk through the lifecycle: pick any of the ten stages to see
   what red teaming looks like there, which of the four components it belongs to, the responsible-AI
   principles at stake, example activities and controls. Every activity, control and principle
   expands into a plain-English explanation. Includes concept primers and a 12-term glossary.
3. **Attack Library** — eight red-teaming techniques (prompt injection, jailbreak, data poisoning,
   model inversion, membership inference, bias exploitation, misuse/repurposing, adversarial
   examples), each tagged with the RAI principle it threatens, its A4SRAI stage, how to test for it,
   and the **29 controls** that mitigate them (hover any control for how to implement it).
   Defensive framing throughout.
4. **Safe Sandbox** — watch a deliberately weak demo bot (VulnBot) fail an attack, then watch a
   named control block it. All eight techniques are covered. Everything is simulated and
   illustrative — **no working exploit payloads**.
5. **Threat-Modelling Wizard** — turn **your own** system (or one of four practice scenarios:
   HireFast, MediBot, NeoBank Assistant, CityWatch) into concrete risks: copy a tailored GenAI
   prompt, add risks one at a time, or paste a Markdown/CSV table back in.
6. **Risk Register** — an editable register (dropdowns for stage / RAI principle / attack type /
   likelihood / impact) with a live **3×3 risk matrix** (Score = Likelihood × Impact, 1–9), a
   severity-sorted view, and CSV export.
7. **Lifecycle Board** — your findings placed on the A4SRAI lifecycle as tier-coloured cards, with a
   **deployment gate** that stays blocked while any high-severity finding is open.
8. **Coverage & Standards** — a blind-spot **coverage grid** (4 components × 8 RAI principles = 32
   cells) plus a mapping of each A4SRAI component to the **EU AI Act**, **NIST AI RMF** and
   **ISO/IEC 42001**.
9. **Knowledge Check** — an 8-question pre-assessment, a post-assessment with per-question feedback
   and a learning-gain score, and a downloadable **certificate (PDF)**.
10. **Report & Export** — a red-team **report** (PDF *and* Markdown), register CSV, and **Save /
    Restore session** so your work survives a refresh or moves between machines.

---

## 1. Deploying to GitHub Pages

### Option A — web interface (no command line)

1. Create a new repository on GitHub (public, e.g. `redloop-browser`).
2. Click **Add file → Upload files** and upload **`index.html`**, **`README.md`** and
   **`.nojekyll`**.
3. Commit to the `main` branch.
4. Go to **Settings → Pages**.
5. Under **Build and deployment → Source**, choose **Deploy from a branch**.
6. Select branch **`main`**, folder **`/ (root)`**, then **Save**.
7. Wait about a minute, then open `https://<your-username>.github.io/<your-repo>/`.

### Option B — command line

```bash
git init
git add index.html README.md .nojekyll
git commit -m "RedLoop-Browser"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

Then enable Pages as in steps 4–7 above.

> **Why `.nojekyll`?** GitHub Pages runs Jekyll by default, which ignores files and folders starting
> with an underscore. The empty `.nojekyll` file turns that off and guarantees your files are served
> exactly as uploaded. Keep it even though this build currently has no underscore-prefixed files.
>
> **macOS tip:** Finder hides dot-files, and dragging one into GitHub's uploader can silently drop
> the leading dot (leaving a useless `nojekyll`). If that happens, use **Add file → Create new
> file**, type `.nojekyll` as the name, leave the body empty and commit.

### Using a project subfolder or custom domain

No change is needed. Every asset is inlined in `index.html`, and there are no absolute paths, so the
app works at any URL depth and on a custom domain.

---

## 2. Running it locally

Because everything is inlined in one file, you can simply **double-click `index.html`** and it opens
in your browser — no web server required, and it works with no internet connection.

If you prefer to serve it (useful for testing clipboard behaviour, which some browsers restrict on
`file://`):

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

---

## 3. Files

| File | Purpose |
|------|---------|
| `index.html` | **The entire application** — HTML, CSS, JavaScript, all learning content and the A4SRAI diagram, inlined in a single self-contained file (~180 KB) |
| `README.md` | This file |
| `LICENSE` | Apache License 2.0 (see [§8](#8-licence)) |
| `.nojekyll` | Tells GitHub Pages to serve files verbatim |

There is no `requirements.txt`, no `package.json`, no build step and no dependency of any kind.

---

## 4. Suggested flow

1. On **Home**, enter your name and take the **pre-assessment** (Knowledge Check → tab 1).
2. Work through **Learn A4SRAI**, the **Attack Library** and the **Safe Sandbox**.
3. Use the **Threat-Modelling Wizard** to turn a system into risks (type them in, or paste a table
   from your GenAI).
4. In the **Risk Register**, set likelihood/impact and **Generate risk matrix**.
5. Review the **Lifecycle Board** and **Coverage & Standards** to spot blind spots and clear the
   deployment gate.
6. Take the **post-assessment**, download your **certificate**, and export a **report** on the
   Report & Export page.
7. Use **Save session (JSON)** to keep a portable copy; **Restore** it later to continue.

As you finish each section, click its **"Mark … complete"** button — the progress bar on Home and in
the sidebar tracks your 8 modules.

### Handing the browser to the next learner

On **Home**, next to *Start learning*, there is a **↻ Restart course** button. It clears everything
this browser holds — the learner's name, all 8 module completions, every risk register, the stage
you had open and both assessment scores — so the next person begins from a genuinely clean slate.

Because that is irreversible, it asks you to confirm first. If the current learner wants to keep
their work, cancel and use **Save session (JSON)** on the Report & Export page, then restart; they
can **Restore** that file later on any machine. This makes a single shared laptop or a lab machine
safe to reuse between learners.

---

## 5. Notes

- **Offline & private.** There are no API calls, no CDNs, no analytics and no cookies. The only
  external references in the whole app are two ordinary hyperlinks you can choose to click (the IEEE
  Computer article and a Responsible AI explainer). Everything else — including the A4SRAI diagram —
  is embedded in the page.
- **Your work stays on your device.** The register, progress and assessment scores live in your
  browser only.
- **Automatic local save.** In addition to the manual **Save / Restore session** JSON (identical to
  the Streamlit version), this build keeps an automatic copy in your browser's `localStorage`, so a
  refresh no longer loses your work. If storage is unavailable (private browsing, strict settings),
  the app still runs normally — it just falls back to manual save/restore. Use **Save session
  (JSON)** to move work between browsers or machines, or to keep a backup.
- **PDF export needs nothing.** The red-team report and the certificate are generated in the browser
  by a small built-in PDF writer, so there is no `reportlab` equivalent to install and no
  Markdown/HTML fallback tier — you always get a real PDF. Markdown and CSV exports are also
  provided.
- **Multi-learner use.** Each visitor's browser is its own isolated session, so registers and
  progress never mix between people. Share the Pages URL with a cohort and everyone works
  independently. On a *shared* machine, use **↻ Restart course** on Home between learners.
- **Nothing to uninstall.** The only thing RedLoop-Browser stores is a single `localStorage` entry
  (`redloop-browser-state-v1`). There are no cookies, no `sessionStorage`, no IndexedDB and no
  service worker. **Restart course** removes that entry outright, so it leaves nothing behind.
- **Accessibility.** Keyboard-navigable, semantic headings and landmarks, a skip link, live-region
  status messages, alt text on the diagram, and automatic light/dark theming that follows your
  system setting.
- **Browser support.** Any current version of Chrome, Edge, Firefox or Safari, on desktop or mobile.
  The layout is responsive and the sidebar collapses above the content on small screens.

---

## 6. Differences from the Streamlit version

This is a faithful port: all ten sections, all content, all controls and all exports are present and
behave the same way. The differences are only where the browser can do better than a Streamlit
server, or where a Python dependency no longer applies:

| Area | Streamlit `app.py` | RedLoop-Browser |
|------|--------------------|-----------------|
| Hosting | Needs Python + `streamlit run` | Static file; GitHub Pages or double-click |
| Session on refresh | Lost unless you saved JSON | Auto-restored from `localStorage`; JSON save/restore still available |
| PDF report & certificate | Requires `reportlab`, else Markdown/HTML fallback | Always available, generated in-browser |
| Risk matrix & coverage grid | Matplotlib PNG | Crisp inline SVG (same colours, layout and thresholds) |
| Register editor | `st.data_editor` grid | HTML table with the same dropdown vocabularies, plus per-row delete |
| Theme | Streamlit default | Follows your system light/dark setting |

Everything else — the A4SRAI content, the ten stages, the eight attacks and 29 controls, the four
scenarios, the GenAI prompt wording, the paste parser, the scoring rules, the deployment-gate logic,
the coverage maths, the 8-question assessment bank and the session-JSON format — is identical.
Session files are interchangeable between the two versions.

---

## 7. Troubleshooting

- **Page is blank on GitHub Pages** — give it a minute after enabling Pages, then hard-refresh
  (`Ctrl/Cmd + Shift + R`). Check **Settings → Pages** shows a green "Your site is live" banner, and
  that the file is named exactly `index.html` at the repository root.
- **404 after enabling Pages** — the branch or folder is wrong. It must be `main` + `/ (root)` (or
  `/docs` if you put `index.html` in a `docs/` folder).
- **My work disappeared** — you may be in private/incognito browsing, or clearing site data on exit,
  which prevents the automatic local save. Use **Save session (JSON)** on the Report & Export page
  and **Restore** it next time.
- **Copy button does nothing** — some browsers block clipboard access on `file://` pages. Serve the
  file over `http://localhost` (see §2) or select the text and copy manually.
- **Certificate button is greyed out** — complete the post-assessment and enter a name first.
- **"Couldn't find any risks to add"** — your pasted table needs a **Risk** column (a Markdown pipe
  table or CSV both work).
- **The previous learner's work is still showing** — click **↻ Restart course** on the Home page and
  confirm. A browser refresh alone will not clear it, because progress is deliberately preserved
  across refreshes.
- **I restarted by mistake** — if you saved a session JSON beforehand, restore it on the Report &
  Export page. Otherwise the data is gone; the confirmation step exists precisely because the reset
  cannot be undone.
- **GitHub Pages shows 404 and the Actions tab redirects to "new workflow"** — that redirect means
  no Pages build has ever run. Commit any change to `main` to trigger one, or toggle **Settings →
  Pages → Source** to *None*, save, then back to *Deploy from a branch* (`main`, `/ (root)`). Also
  confirm your GitHub account email is verified, as Pages will not build otherwise.

---

## 8. Licence

RedLoop-Browser is released under the **Apache License, Version 2.0**. The full text is in the
[`LICENSE`](LICENSE) file, and the canonical copy is at
<https://www.apache.org/licenses/LICENSE-2.0>.

In short, you may use, modify, distribute and build commercial work on RedLoop-Browser, including
inside your own organisation, provided you:

- keep the copyright and licence notice with any substantial portion you redistribute;
- state clearly which files you changed, if you distribute a modified version; and
- accept that the software is provided **"as is", without warranties or conditions of any kind**.

Apache-2.0 also grants you a patent licence from the contributors, which terminates if you bring a
patent claim alleging the software infringes your patents.

**Trademarks and framework name.** The licence covers the software; it does **not** grant rights to
the names **RedLoop**, **RedLoop-Browser** or **A4SRAI**, or to any associated marks (Apache-2.0,
§6). If you publish a modified version, please give it a different name so learners can tell the
frameworks apart.

**Instructional content.** The learning material — stage explanations, the 29 control descriptions,
the four scenarios, the glossary and the assessment bank — is covered by the same Apache-2.0 grant.
Educators reusing it in courses are asked, but not required, to cite the IEEE Computer article
below.

**Not legal advice.** The mapping of A4SRAI components to the EU AI Act, NIST AI RMF and
ISO/IEC 42001 is illustrative only and is not legal or compliance advice.

---

## 9. Credits & citation

RedLoop and the **A4SRAI (Agile 4 Secure Responsible AI)** framework are the work of
**Dr Somdip Dey**. The framework is published in IEEE Computer:
[Implementing AI Red Teaming to Develop Secure Responsible AI Models](https://ieeexplore.ieee.org/abstract/document/11220004).

If you use RedLoop-Browser in teaching or research, please cite that article.

RedLoop-Browser never displays working attack payloads or harmful content — only before/after
behaviour, so learners gain the disposition to think like an attacker without a usable capability to
act as one.

Copyright © Dr Somdip Dey 2026. Licensed under the Apache License, Version 2.0.
