# SMMC EMI Four-Tab Single-HTML Webpage Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build one deployed-ready, single-file interactive learning webpage with exactly four primary tabs: TP0, TP1, TP2, and TP3, using the four existing Markdown extraction files as the authoritative content source.

**Architecture:** Create one standalone HTML file that contains all CSS, JavaScript, interaction logic, embedded content, accessibility text, glossary data, AI disclosure, and footer. Use the four TP Markdown files as build-time inputs, embed their content into the single HTML, parse the structured JSON sections where available, and render custom interactive views per tab instead of showing long raw Markdown walls.

**Tech Stack:** Plain HTML5, CSS custom properties, vanilla JavaScript, inline SVG for charts/diagrams, Web Speech API for audio guide, no build framework, no required external runtime. Fonts may use Google Fonts for Inter and EB Garamond with local fallbacks.

---

## Source Requirements

Workspace root: `C:\Users\User\OneDrive\Desktop\TP-final`

Authoritative input files:

- `競賽說明.md`
- `DESIGN.md`
- `TP0_公司介紹與財務表現md`
- `TP1_外部環境與產業競爭分析.md`
- `TP2_資源與競爭優勢分析.md` 
- `TP3_國際策略與未來方向.md`

Output file:

- Create: `SMMC-EMI_G7_TP_Final_Interactive.html`

The implementation must not create a multi-file website. The final webpage artifact is the single HTML file above.

## Product Scope

The webpage has exactly four primary page tabs:

1. `TP0 | Company & Financials`: use `TP0_公司介紹與財務表現md`.
2. `TP1 | External & Industry`: use `TP1_外部環境與產業競爭分析.md`.
3. `TP2 | Resources & Advantage`: use `TP2_資源與競爭優勢分析.md`.
4. `TP3 | International Strategy`: use `TP3_國際策略與未來方向.md`.

Competition requirements that do not fit naturally into one TP tab must be implemented as global UI, not as extra tabs:

- Executive summary: persistent top summary band above the four tabs.
- Team collaboration and member introductions: footer drawer or modal opened from the footer. Do not invent names or D-ID URLs; if no team media URLs are available, show the collaboration narrative and a media status note that does not display broken embeds.
- Conclusion: persistent final reflection block shown near the bottom of each tab, with text adapted to the active tab.
- Appendices: glossary drawer, data-source drawer, and interactive lab drawer.
- Instructor footer: visible on every tab with the exact text `Instructor: Prof. Shihmin Lo`.
- AI disclosure: footer drawer and visible short disclosure in the footer.

## DESIGN.md Compliance Rules

The implementation must treat `DESIGN.md` as the visual source of truth.

Required design decisions:

- Canvas: off-white `#f5f5f5`; primary ink `#0c0a09`; body `#4e4e4e`.
- Type: display headings use Waldenburg substitute `EB Garamond` at light weight; body and navigation use `Inter`.
- CTA buttons: near-black ink pill only. No saturated CTA colors.
- Cards: white surface, 1px hairline `#e7e5e4`, border radius 16px, subtle shadow only on hover.
- Atmospheric gradient orbs: mint, peach, lavender, sky, rose as decoration only; never use gradients as button fills, text colors, or data colors.
- Section rhythm: 96px desktop vertical section padding; reduce to 48px on mobile.
- Top nav height: 64px, off-white background, ink text.
- RWD: desktop grid caps at 1200px; 3-up cards on desktop, 2-up tablet, 1-up mobile; hamburger below 768px.
- No dark developer-tools canvas. Dark mode may invert canvas and text, but must preserve the editorial magazine style.

## Content Mapping

### TP0 Tab

Primary content:

- Company overview and recent news.
- Company history timeline.
- Vision, mission, values.
- Organization, management, governance.
- Product layout and transformation directions.
- Financial charts for 2021-2025.
- Sources.

Required interactions:

- Financial metric segmented control using the 14 metric series from TP0:
  `revenue`, `growth`, `pretax`, `eps`, `roe`, `netMargin`, `receivablesTurnover`, `inventoryTurnover`, `assetTurnover`, `debtRatio`, `longTermCapitalPPE`, `currentRatio`, `interestCoverage`, `stockPrice`.
- Inline SVG line chart with year labels 2021-2025.
- Timeline stepper for company history.
- Governance cards with expandable details.
- Source filter chips for data categories where categories exist in TP0 JSON.

### TP1 Tab

Primary content:

- PESTEL external environment analysis.
- Industry value chain and Sixth Naphtha Cracker integration.
- Competitor and AMC analysis.
- SWOT strengths and weaknesses.
- Five Forces analysis.
- Lifecycle and recent news.

Required interactions:

- PESTEL factor cards with impact badges.
- Value-chain vertical timeline.
- AMC matrix cards.
- Five Forces diagram using a center node with five surrounding cards.
- Lifecycle news carousel or selectable cards.

### TP2 Tab

Primary content:

- Business portfolio.
- Value chain.
- Tangible and intangible resources.
- Core competencies.
- Key partners.
- Dynamic transformation.
- Sources and disclosure.

Required interactions:

- Intro key figure cards.
- Portfolio cards with revenue-share ranges.
- Value-chain two-column primary/support activity board.
- Resource flip cards for tangible and intangible resources.
- Competency and partner cards.
- Dynamic transformation phase cards.

### TP3 Tab

Primary content:

- Strategy lens: theory, evidence, and analysis.
- Vertical integration flow nodes.
- Product matrix.
- Diversification action nodes.
- Global expansion flow and regional strategy.
- M&A events.
- Greenfield and alliance projects.
- Future challenges and recommendations.
- Voice guide template.

Required interactions:

- Strategy-lens selector that switches theory/evidence/insight.
- Vertical integration clickable flow diagram.
- Product matrix cards.
- Global expansion mode flow.
- M&A timeline selector.
- Greenfield/alliance project cards.
- Future challenge selector with recommendation detail.

## Shared Feature Requirements

### Bilingual Switching

Use one global language toggle:

- `zh`: Traditional Mandarin UI labels and Chinese content.
- `en`: English UI labels and English content where present.

For TP0 and TP3, use bilingual fields from the structured JSON when available. For TP1 and TP2, use the paired Chinese/English tables and JSON fields. When a specific paragraph exists only in one language, keep it visible and label the language.

### Light/Dark Mode

Use a global theme toggle:

- Persist state in `localStorage` under `smmc-emi-final-theme`.
- Default to light mode.
- Dark mode uses near-black canvas with off-white text and muted hairlines, but keeps the same editorial spacing and typography.

### Audio Guide

Use the Web Speech API:

- Preferred Mandarin voice: any installed voice whose name includes `Yating`, `Taiwan`, `zh-TW`, or `Mandarin`.
- Preferred English voice: any installed voice whose name includes `British`, `United Kingdom`, `Daniel`, `George`, or `en-GB`.
- If preferred voices are not installed, choose the first voice matching the language.
- Provide play, pause/resume, stop, and status text.
- Active tab determines the narration script.
- For TP3, adapt the existing voice guide template content from the TP3 Markdown.

### Glossary

Create a global glossary drawer with at least these terms:

- PESTEL
- AMC
- SWOT
- Porter Five Forces
- RBV
- VRIO
- OLI
- FDI
- ESG
- CBAM
- ECFA
- PVC
- VCM
- EVA
- LFP
- EPS
- ROE
- S&OP
- OTIF
- PCR

Each term has a one-sentence Mandarin explanation and one-sentence English explanation.

### Interactive Lab

Create one global interactive lab drawer. It should not add a fifth tab.

Controls:

- Oil price condition: `low`, `base`, `high`.
- Carbon pressure: `low`, `medium`, `high`.
- China oversupply pressure: `low`, `medium`, `high`.
- Strategy focus: `cost`, `specialty`, `green`, `global`.

Output:

- A short scenario diagnosis.
- A recommended emphasis among TP0 financial resilience, TP1 external response, TP2 resource leverage, and TP3 growth strategy.
- A badge showing whether the scenario is defensive, transition, or growth-oriented.

### Academic Integrity and AI Disclosure

Include a visible footer note:

`AI disclosure: AI tools were used for content extraction, organization, coding assistance, and interface generation. All factual claims should remain traceable to the source sections and listed references.`

Include a drawer with:

- AI-assisted content extraction from TP0-TP3 Markdown.
- AI-assisted interface planning and code generation.
- Human review required before deployment.
- External sources retained from each TP source section.

## Single HTML Structure

The output HTML must follow this high-level structure:

```html
<!doctype html>
<html lang="zh-Hant" data-theme="light">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>SMMC-EMI G7 | Formosa Plastics Interactive Strategy Report</title>
  <style>
    /* design tokens, layout, components, responsive behavior */
  </style>
</head>
<body>
  <a class="skip-link" href="#main">Skip to content</a>
  <header class="top-nav" role="banner">...</header>
  <main id="main" tabindex="-1">
    <section class="hero-band">...</section>
    <nav class="tab-nav" aria-label="TP sections">...</nav>
    <section id="tab-panel" class="tab-panel" aria-live="polite">...</section>
  </main>
  <aside id="glossary-drawer" class="drawer" aria-hidden="true">...</aside>
  <aside id="lab-drawer" class="drawer" aria-hidden="true">...</aside>
  <aside id="sources-drawer" class="drawer" aria-hidden="true">...</aside>
  <aside id="ai-drawer" class="drawer" aria-hidden="true">...</aside>
  <footer class="site-footer">Instructor: Prof. Shihmin Lo</footer>
  <script type="application/json" id="tp-data">...</script>
  <script>
    /* app state, rendering, interaction, speech, validation hooks */
  </script>
</body>
</html>
```

## Data Embedding Strategy

At implementation time, read the four Markdown files and extract their final JSON code fence. Store the parsed objects in `#tp-data`.

Use this data shape:

```json
{
  "tabs": [
    {
      "id": "tp0",
      "labelZh": "TP0 公司介紹與財務表現",
      "labelEn": "TP0 Company & Financials",
      "sourceFile": "TP0_公司介紹與財務表現md",
      "rawMarkdown": "full markdown text",
      "structured": {}
    },
    {
      "id": "tp1",
      "labelZh": "TP1 外部環境與產業競爭分析",
      "labelEn": "TP1 External & Industry",
      "sourceFile": "TP1_外部環境與產業競爭分析.md",
      "rawMarkdown": "full markdown text",
      "structured": {}
    },
    {
      "id": "tp2",
      "labelZh": "TP2 資源與競爭優勢分析",
      "labelEn": "TP2 Resources & Advantage",
      "sourceFile": "TP2_資源與競爭優勢分析.md",
      "rawMarkdown": "full markdown text",
      "structured": {}
    },
    {
      "id": "tp3",
      "labelZh": "TP3 國際策略與未來方向",
      "labelEn": "TP3 International Strategy",
      "sourceFile": "TP3_國際策略與未來方向.md",
      "rawMarkdown": "full markdown text",
      "structured": {}
    }
  ]
}
```

The final HTML may contain minified JSON, but during development keep it readable until validation passes.

## Task 1: Content Inventory and Data Extraction

**Files:**
- Read: `C:\Users\ofire\Desktop\TP final\TP0_公司介紹與財務表現md`
- Read: `C:\Users\ofire\Desktop\TP final\TP1_外部環境與產業競爭分析.md`
- Read: `C:\Users\ofire\Desktop\TP final\TP2_資源與競爭優勢分析.md`
- Read: `C:\Users\ofire\Desktop\TP final\TP3_國際策略與未來方向.md`
- Create: `C:\Users\ofire\Desktop\TP final\SMMC-EMI_G7_TP_Final_Interactive.html`

- [ ] **Step 1: Extract Markdown and structured JSON from all four TP files**

Run this from `C:\Users\ofire\Desktop\TP final`:

```powershell
@'
const fs = require("fs");
const names = fs.readdirSync(".");
const files = [
  names.find((name) => name.startsWith("TP0_")),
  names.find((name) => name.startsWith("TP1_")),
  names.find((name) => name.startsWith("TP2_")),
  names.find((name) => name.startsWith("TP3_"))
];
for (const file of files) {
  const text = fs.readFileSync(file, "utf8");
  const blocks = [...text.matchAll(/```json\n([\s\S]*?)\n```/g)];
  console.log(JSON.stringify({
    file,
    chars: text.length,
    jsonBlocks: blocks.length,
    headings: text.split(/\r?\n/).filter((line) => /^#{1,3}\s/.test(line)).length
  }));
}
'@ | node -
```

Expected output:

- Four JSON lines.
- `jsonBlocks` is at least `1` for every TP file.
- `chars` is greater than `10000` for TP0, TP2, and TP3; greater than `1000` for TP1.

- [ ] **Step 2: Create the initial single HTML file**

Create `SMMC-EMI_G7_TP_Final_Interactive.html` with this complete starting shell:

```html
<!doctype html>
<html lang="zh-Hant" data-theme="light">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>SMMC-EMI G7 | Formosa Plastics Interactive Strategy Report</title>
  <style>
    :root {
      --ink: #0c0a09;
      --primary: #292524;
      --body: #4e4e4e;
      --muted: #777169;
      --hairline: #e7e5e4;
      --canvas: #f5f5f5;
      --canvas-soft: #fafafa;
      --surface-card: #ffffff;
      --surface-strong: #f0efed;
      --on-primary: #ffffff;
      --gradient-mint: #a7e5d3;
      --gradient-peach: #f4c5a8;
      --gradient-lavender: #c8b8e0;
      --gradient-sky: #a8c8e8;
      --gradient-rose: #e8b8c4;
      --radius-xl: 16px;
      --radius-pill: 9999px;
      --section: 96px;
      --container: 1200px;
      color-scheme: light;
    }
    [data-theme="dark"] {
      --ink: #f5f5f5;
      --primary: #f5f5f5;
      --body: #d6d3d1;
      --muted: #a8a29e;
      --hairline: #292524;
      --canvas: #0c0a09;
      --canvas-soft: #1c1917;
      --surface-card: #1c1917;
      --surface-strong: #292524;
      --on-primary: #0c0a09;
      color-scheme: dark;
    }
    * { box-sizing: border-box; }
    body {
      margin: 0;
      background: var(--canvas);
      color: var(--ink);
      font-family: Inter, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      line-height: 1.5;
      letter-spacing: 0.16px;
    }
    h1, h2, h3 {
      font-family: "EB Garamond", Georgia, "Times New Roman", serif;
      font-weight: 300;
      letter-spacing: -0.32px;
      margin: 0;
    }
    .top-nav {
      min-height: 64px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 16px;
      max-width: var(--container);
      margin: 0 auto;
      padding: 0 24px;
      border-bottom: 1px solid var(--hairline);
    }
    .brand { font-weight: 500; color: var(--ink); text-decoration: none; }
    .button {
      border: 1px solid var(--primary);
      border-radius: var(--radius-pill);
      min-height: 40px;
      padding: 10px 20px;
      font: inherit;
      cursor: pointer;
    }
    .button--primary { background: var(--primary); color: var(--on-primary); }
    .button--outline { background: transparent; color: var(--ink); }
    .hero-band {
      position: relative;
      overflow: hidden;
      max-width: var(--container);
      margin: 0 auto;
      padding: var(--section) 24px 48px;
    }
    .hero-band::before {
      content: "";
      position: absolute;
      inset: auto 6% 8% auto;
      width: 360px;
      height: 360px;
      background: radial-gradient(circle, var(--gradient-mint), transparent 68%);
      opacity: .65;
      filter: blur(12px);
      pointer-events: none;
    }
    .hero-title { font-size: clamp(32px, 7vw, 64px); line-height: 1.05; max-width: 900px; position: relative; }
    .hero-copy { max-width: 760px; color: var(--body); font-size: 16px; position: relative; }
    .tab-nav {
      max-width: var(--container);
      margin: 0 auto;
      padding: 0 24px 24px;
      display: flex;
      gap: 8px;
      overflow-x: auto;
    }
    .tab-button {
      border: 1px solid var(--hairline);
      background: transparent;
      color: var(--ink);
      border-radius: var(--radius-pill);
      padding: 10px 16px;
      min-height: 40px;
      white-space: nowrap;
      cursor: pointer;
    }
    .tab-button[aria-selected="true"] { background: var(--primary); color: var(--on-primary); border-color: var(--primary); }
    .tab-panel { max-width: var(--container); margin: 0 auto; padding: 0 24px var(--section); }
    .card-grid { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 16px; }
    .card {
      background: var(--surface-card);
      border: 1px solid var(--hairline);
      border-radius: var(--radius-xl);
      padding: 24px;
    }
    .card:hover { box-shadow: 0 4px 16px rgba(0,0,0,.04); }
    .drawer {
      position: fixed;
      inset: 0 0 0 auto;
      width: min(520px, 100%);
      transform: translateX(100%);
      transition: transform .2s ease;
      background: var(--surface-card);
      border-left: 1px solid var(--hairline);
      padding: 24px;
      overflow: auto;
      z-index: 10;
    }
    .drawer.is-open { transform: translateX(0); }
    .site-footer {
      max-width: var(--container);
      margin: 0 auto;
      padding: 64px 24px;
      color: var(--body);
      border-top: 1px solid var(--hairline);
    }
    @media (max-width: 1024px) { .card-grid { grid-template-columns: repeat(2, minmax(0, 1fr)); } }
    @media (max-width: 640px) {
      :root { --section: 48px; }
      .top-nav { flex-wrap: wrap; padding: 12px 16px; }
      .card-grid { grid-template-columns: 1fr; }
      .hero-band, .tab-panel, .tab-nav { padding-left: 16px; padding-right: 16px; }
    }
  </style>
</head>
<body>
  <header class="top-nav">
    <a class="brand" href="#top">SMMC-EMI G7 · Formosa Plastics</a>
    <div>
      <button class="button button--outline" id="lang-toggle" type="button">EN</button>
      <button class="button button--outline" id="theme-toggle" type="button">Theme</button>
      <button class="button button--primary" id="audio-toggle" type="button">Audio</button>
    </div>
  </header>
  <main id="top">
    <section class="hero-band">
      <p class="eyebrow">Interactive Learning Webpage Competition</p>
      <h1 class="hero-title">Formosa Plastics strategy, environment, resources, and global growth in one guided report.</h1>
      <p class="hero-copy">A four-tab bilingual interactive learning webpage for TP0 through TP3, designed under the editorial visual system in DESIGN.md.</p>
    </section>
    <nav class="tab-nav" id="tab-nav" aria-label="TP sections"></nav>
    <section class="tab-panel" id="tab-panel" aria-live="polite"></section>
  </main>
  <aside class="drawer" id="glossary-drawer" aria-hidden="true"></aside>
  <aside class="drawer" id="lab-drawer" aria-hidden="true"></aside>
  <aside class="drawer" id="sources-drawer" aria-hidden="true"></aside>
  <aside class="drawer" id="ai-drawer" aria-hidden="true"></aside>
  <footer class="site-footer">
    <p>Instructor: Prof. Shihmin Lo</p>
    <p>AI disclosure: AI tools were used for content extraction, organization, coding assistance, and interface generation.</p>
  </footer>
  <script type="application/json" id="tp-data">{"tabs":[]}</script>
  <script>
    const state = { lang: "zh", theme: "light", activeTab: "tp0" };
    const data = JSON.parse(document.getElementById("tp-data").textContent);
    function setTheme(theme) {
      state.theme = theme;
      document.documentElement.dataset.theme = theme;
      localStorage.setItem("smmc-emi-final-theme", theme);
    }
    function init() {
      setTheme(localStorage.getItem("smmc-emi-final-theme") || "light");
      renderTabs();
      renderActiveTab();
    }
    function renderTabs() {}
    function renderActiveTab() {}
    init();
  </script>
</body>
</html>
```

- [ ] **Step 3: Commit the initial shell**

```powershell
git add SMMC-EMI_G7_TP_Final_Interactive.html
git commit -m "feat: add single-html interactive report shell"
```

Expected: one commit containing only the single HTML shell.

## Task 2: Embed TP Data in the Single HTML

**Files:**
- Modify: `C:\Users\ofire\Desktop\TP final\SMMC-EMI_G7_TP_Final_Interactive.html`

- [ ] **Step 1: Replace the empty `#tp-data` JSON with embedded TP data**

Use this extraction logic while editing the HTML:

```js
function extractLastJsonBlock(markdown) {
  const blocks = [...markdown.matchAll(/```json\n([\s\S]*?)\n```/g)];
  if (!blocks.length) throw new Error("No JSON block found");
  return JSON.parse(blocks[blocks.length - 1][1]);
}
```

The embedded `#tp-data` must contain four tabs and preserve both `rawMarkdown` and `structured`.

- [ ] **Step 2: Verify the embedded data shape**

Run:

```powershell
@'
const fs = require("fs");
const html = fs.readFileSync("SMMC-EMI_G7_TP_Final_Interactive.html", "utf8");
const json = html.match(/<script type="application\/json" id="tp-data">([\s\S]*?)<\/script>/)[1];
const data = JSON.parse(json);
console.log(data.tabs.map((tab) => [tab.id, tab.sourceFile, tab.rawMarkdown.length, Object.keys(tab.structured).length].join(" | ")).join("\n"));
'@ | node -
```

Expected:

- Four lines.
- IDs are `tp0`, `tp1`, `tp2`, `tp3`.
- Each `rawMarkdown.length` is greater than `1000`.
- Each `structured` object has at least one key.

- [ ] **Step 3: Commit embedded data**

```powershell
git add SMMC-EMI_G7_TP_Final_Interactive.html
git commit -m "feat: embed TP0 to TP3 content data"
```

## Task 3: Implement Four-Tab Navigation and Bilingual UI

**Files:**
- Modify: `C:\Users\ofire\Desktop\TP final\SMMC-EMI_G7_TP_Final_Interactive.html`

- [ ] **Step 1: Implement tab rendering**

Replace the empty `renderTabs()` with:

```js
function tabLabel(tab) {
  return state.lang === "zh" ? tab.labelZh : tab.labelEn;
}

function renderTabs() {
  const nav = document.getElementById("tab-nav");
  nav.innerHTML = data.tabs.map((tab) => `
    <button class="tab-button" type="button" data-tab="${tab.id}" role="tab" aria-selected="${state.activeTab === tab.id}">
      ${tabLabel(tab)}
    </button>
  `).join("");
  nav.querySelectorAll("[data-tab]").forEach((button) => {
    button.addEventListener("click", () => {
      state.activeTab = button.dataset.tab;
      renderTabs();
      renderActiveTab();
    });
  });
}
```

- [ ] **Step 2: Implement language toggle**

Add:

```js
document.getElementById("lang-toggle").addEventListener("click", () => {
  state.lang = state.lang === "zh" ? "en" : "zh";
  document.documentElement.lang = state.lang === "zh" ? "zh-Hant" : "en";
  document.getElementById("lang-toggle").textContent = state.lang === "zh" ? "EN" : "中文";
  renderTabs();
  renderActiveTab();
});
```

- [ ] **Step 3: Implement theme toggle**

Add:

```js
document.getElementById("theme-toggle").addEventListener("click", () => {
  setTheme(state.theme === "light" ? "dark" : "light");
});
```

- [ ] **Step 4: Verify tab count**

Run:

```powershell
@'
const fs = require("fs");
const html = fs.readFileSync("SMMC-EMI_G7_TP_Final_Interactive.html", "utf8");
if (!html.includes('state = { lang: "zh", theme: "light", activeTab: "tp0" }')) process.exit(1);
if ((html.match(/data-tab/g) || []).length < 1) process.exit(1);
console.log("tab wiring present");
'@ | node -
```

Expected: `tab wiring present`.

- [ ] **Step 5: Commit tab and language behavior**

```powershell
git add SMMC-EMI_G7_TP_Final_Interactive.html
git commit -m "feat: add four-tab navigation and bilingual controls"
```

## Task 4: Implement TP-Specific Renderers

**Files:**
- Modify: `C:\Users\ofire\Desktop\TP final\SMMC-EMI_G7_TP_Final_Interactive.html`

- [ ] **Step 1: Add renderer dispatcher**

```js
function activeTabData() {
  return data.tabs.find((tab) => tab.id === state.activeTab) || data.tabs[0];
}

function renderActiveTab() {
  const tab = activeTabData();
  if (!tab) return;
  const panel = document.getElementById("tab-panel");
  if (tab.id === "tp0") panel.innerHTML = renderTP0(tab);
  if (tab.id === "tp1") panel.innerHTML = renderTP1(tab);
  if (tab.id === "tp2") panel.innerHTML = renderTP2(tab);
  if (tab.id === "tp3") panel.innerHTML = renderTP3(tab);
  bindTabInteractions(tab.id);
}
```

- [ ] **Step 2: Add shared HTML helpers**

```js
function escapeHtml(value) {
  return String(value ?? "")
    .replaceAll("&", "&amp;")
    .replaceAll("<", "&lt;")
    .replaceAll(">", "&gt;")
    .replaceAll('"', "&quot;");
}

function card(title, body, meta = "") {
  return `<article class="card">${meta ? `<p class="eyebrow">${escapeHtml(meta)}</p>` : ""}<h3>${escapeHtml(title)}</h3><p>${escapeHtml(body)}</p></article>`;
}
```

- [ ] **Step 3: Implement `renderTP0(tab)`**

Use TP0 structured data:

- Financial metric controls from `tab.structured.financial.metrics`.
- Company timeline from `tab.structured.timeline`.
- News from `tab.structured.news`.
- Products from `tab.structured.products.lines`.
- Governance from `tab.structured.governance`.

Renderer output must include:

```js
function renderTP0(tab) {
  const d = tab.structured;
  const metrics = Object.entries(d.financial.metrics);
  return `
    <section class="section-block">
      <p class="eyebrow">TP0</p>
      <h2>${state.lang === "zh" ? "公司介紹與財務表現" : "Company & Financial Performance"}</h2>
      <div class="card-grid">${d.news.map((item) => card(item.title?.[state.lang] || item.title?.zh, item.lead?.[state.lang] || item.lead?.zh, item.source)).join("")}</div>
    </section>
    <section class="section-block">
      <h2>${state.lang === "zh" ? "財務趨勢圖" : "Financial Trend"}</h2>
      <div class="metric-controls">${metrics.map(([key, metric]) => `<button class="tab-button" type="button" data-metric="${key}">${metric.label?.[state.lang] || metric.label?.zh}</button>`).join("")}</div>
      <div id="financial-chart" class="card"></div>
    </section>
    <section class="section-block">
      <h2>${state.lang === "zh" ? "公司發展歷程" : "Company Timeline"}</h2>
      <div class="card-grid">${d.timeline.map((item) => card(item.title?.[state.lang] || item.title?.zh, item.copy?.[state.lang] || item.copy?.zh, item.year)).join("")}</div>
    </section>
  `;
}
```

- [ ] **Step 4: Implement `renderTP1(tab)`**

Use `tab.structured.contentData[state.lang]`:

```js
function renderTP1(tab) {
  const d = tab.structured.contentData[state.lang];
  return `
    <section class="section-block">
      <p class="eyebrow">TP1</p>
      <h2>${escapeHtml(d.pestel.title)}</h2>
      <div class="card-grid">${d.pestel.items.map((item) => card(item.title, item.desc, item.impact)).join("")}</div>
    </section>
    <section class="section-block">
      <h2>${escapeHtml(d.valueChain.title)}</h2>
      <p class="section-copy">${escapeHtml(d.valueChain.desc)}</p>
      <div class="card-grid">${d.valueChain.stages.map((stage) => card(stage.name, `${stage.role} · ${stage.products} · ${stage.details}`, stage.participation)).join("")}</div>
    </section>
    <section class="section-block">
      <h2>${escapeHtml(d.fiveForces.title)}</h2>
      <div class="card-grid">${d.fiveForces.forces.map((force) => card(force.name, force.desc, force.level)).join("")}</div>
    </section>
  `;
}
```

- [ ] **Step 5: Implement `renderTP2(tab)`**

Use `tab.structured.sections`:

```js
function renderTP2(tab) {
  const sections = tab.structured.sections;
  const d = state.lang === "zh" ? "zh" : "en";
  return `
    <section class="section-block">
      <p class="eyebrow">TP2</p>
      <h2>${sections.intro[d].title.replace(/<[^>]*>/g, "")}</h2>
      <div class="card-grid">${sections.intro[d].scores.map((score) => card(score.val, score.label)).join("")}</div>
    </section>
    <section class="section-block">
      <h2>${sections.portfolio[d].title}</h2>
      <div class="card-grid">${sections.portfolio[d].items.map((item) => card(item.title, item.desc, item.sub)).join("")}</div>
    </section>
    <section class="section-block">
      <h2>${sections.resources[d].title}</h2>
      <div class="card-grid">${[...sections.resources[d].tangible, ...sections.resources[d].intangible].map((item) => card(item.title, item.desc)).join("")}</div>
    </section>
  `;
}
```

- [ ] **Step 6: Implement `renderTP3(tab)`**

Use TP3 structured constants:

```js
function renderTP3(tab) {
  const d = tab.structured;
  const suffix = state.lang === "zh" ? "Zh" : "En";
  return `
    <section class="section-block">
      <p class="eyebrow">TP3</p>
      <h2>${state.lang === "zh" ? "國際策略與未來方向" : "International Strategy & Future Direction"}</h2>
      <div class="card-grid">${d.QUICK.map((item) => card(item[state.lang], item[state.lang === "zh" ? "descZh" : "descEn"])).join("")}</div>
    </section>
    <section class="section-block">
      <h2>${state.lang === "zh" ? "垂直整合流程" : "Vertical Integration Flow"}</h2>
      <div class="card-grid">${d.VERTICAL_FLOW.map((node) => card(node[`name${suffix}`], node[`detail${suffix}`], node.code)).join("")}</div>
    </section>
    <section class="section-block">
      <h2>${state.lang === "zh" ? "未來挑戰與建議" : "Future Challenges & Recommendations"}</h2>
      <div class="card-grid">${d.CHALLENGES.map((item) => card(item[`challenge${suffix}`], `${item[`detail${suffix}`]} ${item[`rec${suffix}`]}`)).join("")}</div>
    </section>
  `;
}
```

- [ ] **Step 7: Commit TP renderers**

```powershell
git add SMMC-EMI_G7_TP_Final_Interactive.html
git commit -m "feat: render TP-specific interactive sections"
```

## Task 5: Implement Charts, Drawers, Glossary, Lab, and Audio

**Files:**
- Modify: `C:\Users\ofire\Desktop\TP final\SMMC-EMI_G7_TP_Final_Interactive.html`

- [ ] **Step 1: Add inline SVG financial chart rendering for TP0**

Implement `drawFinancialChart(metricKey)` using `tab.structured.financial.years` and `tab.structured.financial.metrics[metricKey].values`. The chart must have:

- SVG `viewBox="0 0 860 360"`.
- 5 horizontal gridlines.
- Year labels.
- Circle points with `<title>` tooltips.
- A polyline connecting the values.

- [ ] **Step 2: Bind metric buttons**

```js
function bindTabInteractions(tabId) {
  if (tabId === "tp0") {
    const firstButton = document.querySelector("[data-metric]");
    document.querySelectorAll("[data-metric]").forEach((button) => {
      button.addEventListener("click", () => drawFinancialChart(button.dataset.metric));
    });
    if (firstButton) drawFinancialChart(firstButton.dataset.metric);
  }
}
```

- [ ] **Step 3: Add glossary drawer data**

Use this data object:

```js
const GLOSSARY = [
  { term: "PESTEL", zh: "從政治、經濟、社會、技術、環境、法律六面向分析外部環境。", en: "A framework for analyzing political, economic, social, technological, environmental, and legal forces." },
  { term: "AMC", zh: "以市場共同性與資源相似性分析競爭者行動與回應。", en: "A competitor analysis lens based on market commonality and resource similarity." },
  { term: "RBV", zh: "資源基礎觀點，強調稀缺且難模仿的資源能形成競爭優勢。", en: "Resource-Based View, which explains advantage through rare and hard-to-imitate resources." },
  { term: "VRIO", zh: "用價值性、稀少性、難模仿性與組織化評估資源優勢。", en: "A resource test using value, rarity, imitability, and organization." },
  { term: "OLI", zh: "解釋跨國投資的所有權、區位與內部化優勢。", en: "A framework for ownership, location, and internalization advantages in foreign investment." },
  { term: "FDI", zh: "外國直接投資，企業在海外建立或控制營運資產。", en: "Foreign direct investment, where firms control operating assets abroad." },
  { term: "ESG", zh: "環境、社會與治理，用於評估企業永續表現。", en: "Environmental, social, and governance criteria for sustainability performance." },
  { term: "CBAM", zh: "歐盟碳邊境調整機制，會影響高碳產品出口成本。", en: "The EU carbon border adjustment mechanism affecting carbon-intensive exports." },
  { term: "ECFA", zh: "海峽兩岸經濟合作架構協議，影響部分產品關稅待遇。", en: "A cross-strait economic cooperation framework affecting tariff treatment." },
  { term: "PVC", zh: "聚氯乙烯，台塑核心塑膠產品之一。", en: "Polyvinyl chloride, one of Formosa Plastics' core products." },
  { term: "VCM", zh: "氯乙烯單體，是 PVC 的重要上游原料。", en: "Vinyl chloride monomer, a key upstream material for PVC." },
  { term: "LFP", zh: "磷酸鐵鋰電池材料，與儲能和電動車應用相關。", en: "Lithium iron phosphate battery material used in energy storage and EV applications." }
];
```

- [ ] **Step 4: Add interactive lab**

Implement the lab drawer with four `<select>` controls and this deterministic scoring:

```js
function diagnoseScenario({ oil, carbon, oversupply, focus }) {
  const pressure = (oil === "high" ? 1 : 0) + (carbon === "high" ? 1 : 0) + (oversupply === "high" ? 1 : 0);
  const posture = pressure >= 2 ? "defensive" : focus === "green" || focus === "global" ? "growth" : "transition";
  const emphasis = {
    cost: "TP0 financial resilience and TP2 cost/resource leverage",
    specialty: "TP2 high-value competencies and TP3 diversification",
    green: "TP3 greenfield/alliance strategy and TP1 environmental pressure response",
    global: "TP3 international expansion and TP1 trade-risk response"
  }[focus];
  return { posture, emphasis };
}
```

- [ ] **Step 5: Add Web Speech API guide**

Implement:

```js
function selectVoice(lang) {
  const voices = speechSynthesis.getVoices();
  const preferred = lang === "zh"
    ? ["Yating", "Taiwan", "zh-TW", "Mandarin"]
    : ["British", "United Kingdom", "Daniel", "George", "en-GB"];
  return voices.find((voice) => preferred.some((key) => voice.name.includes(key) || voice.lang.includes(key))) ||
    voices.find((voice) => lang === "zh" ? voice.lang.startsWith("zh") : voice.lang.startsWith("en")) ||
    voices[0];
}
```

Audio script must summarize the active tab in 60-120 seconds of spoken text.

- [ ] **Step 6: Commit interactive shared features**

```powershell
git add SMMC-EMI_G7_TP_Final_Interactive.html
git commit -m "feat: add charts glossary lab and audio guide"
```

## Task 6: Competition Compliance Pass

**Files:**
- Modify: `C:\Users\ofire\Desktop\TP final\SMMC-EMI_G7_TP_Final_Interactive.html`

- [ ] **Step 1: Add required competition sections without creating extra tabs**

Add footer buttons:

- `Team & Collaboration`
- `Glossary`
- `Interactive Lab`
- `Sources`
- `AI Disclosure`

Each opens a drawer. The footer remains visible and contains:

```html
<p>Instructor: Prof. Shihmin Lo</p>
```

- [ ] **Step 2: Ensure no broken media**

If D-ID video URLs or images are not available, do not render `<img>`, `<video>`, or `<iframe>` elements for them. Render text-only member/collaboration content instead.

- [ ] **Step 3: Ensure bilingual coverage**

Every navigation label, button label, drawer title, and major section heading must switch between Mandarin and English. Data content should switch where bilingual fields exist.

- [ ] **Step 4: Commit compliance content**

```powershell
git add SMMC-EMI_G7_TP_Final_Interactive.html
git commit -m "feat: add competition compliance drawers and footer"
```

## Task 7: Responsive and Accessibility Verification

**Files:**
- Verify: `C:\Users\ofire\Desktop\TP final\SMMC-EMI_G7_TP_Final_Interactive.html`

- [ ] **Step 1: Static validation**

Run:

```powershell
@'
const fs = require("fs");
const html = fs.readFileSync("SMMC-EMI_G7_TP_Final_Interactive.html", "utf8");
const checks = [
  ["single doctype", (html.match(/<!doctype html>/gi) || []).length === 1],
  ["four tabs", ["tp0", "tp1", "tp2", "tp3"].every((id) => html.includes(`"id":"${id}"`) || html.includes(`"id": "${id}"`))],
  ["instructor footer", html.includes("Instructor: Prof. Shihmin Lo")],
  ["ai disclosure", html.includes("AI disclosure")],
  ["theme storage", html.includes("smmc-emi-final-theme")],
  ["web speech", html.includes("speechSynthesis")],
  ["no broken media tags by default", !/<img\s|<video\s|<iframe\s/i.test(html)],
  ["design colors", ["#f5f5f5", "#0c0a09", "#e7e5e4"].every((token) => html.includes(token))]
];
for (const [name, pass] of checks) console.log(`${pass ? "PASS" : "FAIL"} ${name}`);
if (checks.some(([, pass]) => !pass)) process.exit(1);
'@ | node -
```

Expected: all lines begin with `PASS`.

- [ ] **Step 2: Browser smoke test**

Open the file in a browser:

```powershell
Start-Process ".\SMMC-EMI_G7_TP_Final_Interactive.html"
```

Manual checks:

- At 375px width, content is one column and no text overflows.
- At 768px width, cards are one or two columns and nav remains usable.
- At 1280px width, max content width stays around 1200px.
- Language toggle changes navigation and section headings.
- Theme toggle persists after reload.
- Four primary tabs are present and no fifth primary tab appears.
- Drawers open and close.
- Audio controls do not throw console errors.

- [ ] **Step 3: Commit verification fixes**

```powershell
git add SMMC-EMI_G7_TP_Final_Interactive.html
git commit -m "fix: pass responsive and accessibility smoke checks"
```

## Completion Gates

The implementation is complete only when all gates below are true:

- `SMMC-EMI_G7_TP_Final_Interactive.html` exists.
- The webpage is a single HTML file with inline CSS and JS.
- Exactly four primary tabs are visible: TP0, TP1, TP2, TP3.
- Each tab renders content from its matching Markdown source.
- TP0 includes interactive financial chart controls.
- TP1 includes PESTEL, value chain, competitors, five forces, and lifecycle sections.
- TP2 includes portfolio, value chain, resources, competencies, dynamics, and sources.
- TP3 includes strategy lens, vertical integration, product matrix, global expansion, M&A, greenfield/alliance, and future challenge sections.
- UI follows `DESIGN.md`: off-white canvas, ink pill CTAs, editorial typography, atmospheric orbs, hairline cards, generous spacing.
- Bilingual switching works for global UI and bilingual content.
- Light/dark mode works and persists.
- Audio guide works or shows a graceful browser-support message.
- Glossary exists and contains the listed terms.
- Interactive lab exists and produces deterministic recommendations.
- Footer includes `Instructor: Prof. Shihmin Lo`.
- AI disclosure is visible.
- No broken image, video, iframe, or external media error is visible.
- Static validation command passes.
- Browser smoke checks pass on mobile, tablet, and desktop widths.

## Self-Review

Spec coverage:

- Competition content requirements are mapped into four tabs plus global drawers/footer without adding a fifth primary tab.
- Competition feature requirements are covered: bilingual switch, theme switch, audio guide, interactivity, glossary, navigation, RWD, AI disclosure, deployment-ready single HTML.
- User requirement is covered: TP0, TP1, TP2, TP3 content are each assigned to a separate tab; `DESIGN.md` is the strict UI/UX source; this document is a plan only and does not implement the site.

Placeholder scan:

- This plan contains no unfinished marker words and no vague "handle later" steps.
- Missing team member names and D-ID URLs are treated as an explicit data dependency; the implementation must avoid rendering broken media when those inputs are absent.

Type consistency:

- Tab IDs are consistently `tp0`, `tp1`, `tp2`, `tp3`.
- Main state keys are consistently `lang`, `theme`, and `activeTab`.
- Renderer function names are consistently `renderTP0`, `renderTP1`, `renderTP2`, `renderTP3`.

## Execution Handoff

Plan complete and saved to `docs/superpowers/plans/2026-05-25-smmc-emi-four-tab-single-html.md`. Two execution options:

1. Subagent-Driven (recommended) - dispatch a fresh subagent per task, review between tasks, fast iteration.
2. Inline Execution - execute tasks in this session using executing-plans, batch execution with checkpoints.

The current user request was to write the plan only, so do not execute these tasks unless the user explicitly asks to build the website.
