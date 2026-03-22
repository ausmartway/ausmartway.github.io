# Website Modernization Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rewrite `index.html` as a modern, dark-themed DevSecOps portfolio with terminal hero, card grid projects, and mobile-responsive layout.

**Architecture:** Single self-contained `index.html` with inline `<style>` and `<script>` blocks. No Jekyll layouts, no build tools, no JS frameworks. Google Fonts via CDN. Fully GitHub Pages compatible.

**Tech Stack:** HTML5, vanilla CSS (custom properties, Grid, Flexbox, `backdrop-filter`), vanilla JS (typewriter animation, hamburger toggle), Google Fonts (Inter + JetBrains Mono).

---

## File Structure

| File | Action | Responsibility |
|---|---|---|
| `index.html` | **Rewrite** | Entire page — structure, styles, and scripts |

No other files touched. `_config.yml`, `_pages/`, `_projects/`, `about.md`, `projects.md` are untouched.

---

## Verification Approach

This is a static HTML file — no unit tests. Verification is visual: open the file directly in a browser (`file:///.../index.html`) or via `python3 -m http.server 8080`. Use Playwright MCP tools to take screenshots for automated verification.

---

## Task 1: Document Skeleton + CSS Foundation

**Files:**
- Rewrite: `index.html`

Build the complete `<head>` with Google Fonts, CSS custom properties, and base reset. Create empty `<body>` with placeholder section comments. No content yet — just the foundation.

- [ ] **Step 1: Replace index.html with the skeleton**

Write `index.html` with this exact content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Yulei Liu — DevSecOps and Cloud Infrastructure Professional. HashiCorp, Terraform, Vault, Go. Based in Sydney, Australia.">
  <title>Yulei Liu — DevSecOps Professional</title>

  <!-- Google Fonts preconnect -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">

  <style>
    /* ── Reset ── */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    /* ── Custom Properties ── */
    :root {
      --bg:      #0d1117;
      --surface: #161b22;
      --border:  #30363d;
      --text:    #e6edf3;
      --muted:   #8b949e;
      --blue:    #58a6ff;
      --green:   #3fb950;
      --orange:  #f78166;
      --purple:  #d2a8ff;
      --yellow:  #e3b341;
    }

    /* ── Base ── */
    html { scroll-behavior: smooth; }
    body {
      background: var(--bg);
      color: var(--text);
      font-family: 'Inter', sans-serif;
      font-size: 15px;
      line-height: 1.6;
    }

    /* ── Shared: Section Labels and Titles ── */
    .section-label {
      font-family: 'JetBrains Mono', monospace;
      font-size: 12px;
      color: var(--muted);
      letter-spacing: 0.08em;
      text-transform: uppercase;
      margin-bottom: 6px;
    }
    .section-title {
      font-size: 22px;
      font-weight: 700;
      color: var(--text);
      margin-bottom: 24px;
      padding-bottom: 12px;
      border-bottom: 1px solid var(--border);
    }

    /* ── Shared: Buttons ── */
    .btn-primary {
      background: #238636;
      color: var(--text);
      border: 1px solid #2ea043;
      padding: 9px 18px;
      border-radius: 6px;
      font-size: 14px;
      font-weight: 500;
      text-decoration: none;
      display: inline-block;
      transition: background 0.2s;
    }
    .btn-primary:hover { background: #2ea043; }

    .btn-ghost {
      background: var(--surface);
      color: var(--blue);
      border: 1px solid var(--border);
      padding: 9px 18px;
      border-radius: 6px;
      font-size: 14px;
      font-weight: 500;
      text-decoration: none;
      display: inline-block;
      transition: border-color 0.2s;
    }
    .btn-ghost:hover { border-color: var(--blue); }

    /* ── Shared: Language Badge ── */
    .lang-badge {
      font-family: 'JetBrains Mono', monospace;
      font-size: 11px;
      color: var(--green);
      background: rgba(63,185,80,0.1);
      border: 1px solid rgba(63,185,80,0.3);
      padding: 2px 8px;
      border-radius: 20px;
    }

    /* ── Shared: Focus Tag ── */
    .focus-tag {
      font-size: 11px;
      color: var(--muted);
    }

    /* ── Shared: Section wrapper ── */
    .section {
      max-width: 860px;
      margin: 0 auto 64px;
      padding: 0 32px;
    }

    /* ── Cursor blink ── */
    @keyframes blink { 50% { opacity: 0; } }
    .cursor {
      display: inline-block;
      width: 9px;
      height: 16px;
      background: var(--blue);
      vertical-align: middle;
      animation: blink 1s step-end infinite;
    }

    /* ── Mobile base ── */
    @media (max-width: 600px) {
      .section-title { font-size: 18px; }
    }
  </style>
</head>
<body>

  <!-- NAV: Task 2 -->
  <!-- HERO: Task 3 -->
  <!-- EXPERTISE: Task 5 -->
  <!-- PROJECTS: Task 6 -->
  <!-- CONTACT+FOOTER: Task 7 -->

  <script>
    // JS added in Tasks 2 and 4
  </script>
</body>
</html>
```

- [ ] **Step 2: Verify the skeleton loads**

Open `index.html` in a browser. Expected: blank dark page (`#0d1117` background), no console errors, Google Fonts loads in Network tab.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add html skeleton with css foundation and custom properties"
```

---

## Task 2: Sticky Navigation

**Files:**
- Modify: `index.html`

Add the nav bar with desktop inline links and mobile hamburger. Includes vanilla JS toggle.

- [ ] **Step 1: Add nav CSS inside the `<style>` block (append before `</style>`)**

```css
/* ── Nav ── */
nav {
  position: sticky;
  top: 0;
  z-index: 100;
  background: rgba(13,17,23,0.85);
  -webkit-backdrop-filter: blur(12px);
  backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--border);
  padding: 0 32px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 56px;
}
.nav-brand {
  font-family: 'JetBrains Mono', monospace;
  font-size: 14px;
  color: var(--green);
  text-decoration: none;
}
.nav-links {
  display: flex;
  gap: 28px;
  list-style: none;
}
.nav-links a {
  color: var(--muted);
  text-decoration: none;
  font-size: 14px;
  transition: color 0.2s;
}
.nav-links a:hover { color: var(--text); }
.nav-hamburger {
  display: none;
  background: none;
  border: none;
  color: var(--muted);
  font-size: 20px;
  cursor: pointer;
  padding: 4px 8px;
}
.nav-dropdown {
  display: none;
  position: absolute;
  top: 56px;
  left: 0;
  right: 0;
  background: var(--surface);
  border-bottom: 1px solid var(--border);
  z-index: 101;
}
.nav-dropdown a {
  display: block;
  color: var(--muted);
  text-decoration: none;
  font-size: 15px;
  padding: 12px 24px;
  transition: color 0.2s;
}
.nav-dropdown a:hover { color: var(--text); }
nav.open .nav-dropdown { display: block; }

@media (max-width: 600px) {
  .nav-links { display: none; }
  .nav-hamburger { display: block; }
}
```

- [ ] **Step 2: Replace `<!-- NAV: Task 2 -->` with nav HTML**

```html
<nav id="main-nav">
  <a href="#" class="nav-brand">~/yuleiliu</a>
  <ul class="nav-links">
    <li><a href="#expertise">Expertise</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <button class="nav-hamburger" id="hamburger" aria-label="Toggle menu">&#9776;</button>
  <div class="nav-dropdown" id="nav-dropdown">
    <a href="#expertise" class="dropdown-link">Expertise</a>
    <a href="#projects" class="dropdown-link">Projects</a>
    <a href="#contact" class="dropdown-link">Contact</a>
  </div>
</nav>
```

- [ ] **Step 3: Add hamburger JS inside the `<script>` block**

```js
(function () {
  var nav = document.getElementById('main-nav');
  var hamburger = document.getElementById('hamburger');

  hamburger.addEventListener('click', function () {
    nav.classList.toggle('open');
  });

  document.querySelectorAll('.dropdown-link').forEach(function (link) {
    link.addEventListener('click', function () {
      nav.classList.remove('open');
    });
  });

  document.addEventListener('click', function (e) {
    if (!nav.contains(e.target)) nav.classList.remove('open');
  });
}());
```

- [ ] **Step 4: Verify desktop nav**

Open in browser at 1280px wide. Expected: sticky frosted nav, `~/yuleiliu` in green on left, Expertise/Projects/Contact in muted on right. Scroll down — nav stays at top.

- [ ] **Step 5: Verify mobile nav**

Resize to 390px wide (DevTools). Expected: nav links hidden, ☰ visible. Tap ☰ opens dropdown. Tap a link or outside — closes dropdown.

- [ ] **Step 6: Commit**

```bash
git add index.html
git commit -m "feat: add sticky nav with mobile hamburger toggle"
```

---

## Task 3: Terminal Hero (Static Structure)

**Files:**
- Modify: `index.html`

Build the terminal window with all content rendered statically. The typewriter (Task 4) will clear and re-animate it. Rendering statically first lets us verify layout before adding animation.

- [ ] **Step 1: Add hero CSS inside `<style>` block**

```css
/* ── Hero ── */
.hero {
  max-width: 860px;
  margin: 72px auto 56px;
  padding: 0 32px;
}
.terminal {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 8px 32px rgba(0,0,0,0.4);
}
.terminal-bar {
  background: #21262d;
  padding: 12px 16px;
  display: flex;
  align-items: center;
  gap: 8px;
  border-bottom: 1px solid var(--border);
}
.dot { width: 12px; height: 12px; border-radius: 50%; flex-shrink: 0; }
.dot-red    { background: #ff5f57; }
.dot-yellow { background: #febc2e; }
.dot-green-dot  { background: #28c840; }
.terminal-title {
  margin: 0 auto;
  font-family: 'JetBrains Mono', monospace;
  font-size: 12px;
  color: var(--muted);
}
.terminal-body {
  padding: 24px 28px 28px;
  font-family: 'JetBrains Mono', monospace;
  font-size: 14px;
  line-height: 1.9;
  overflow-x: auto;
}
.t-prompt { color: var(--green); }
.t-cmd    { color: var(--blue); }
.t-key    { color: var(--purple); }
.t-val    { color: var(--orange); }
.t-block  { margin-left: 16px; }
.hero-cta {
  margin-top: 24px;
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
}
```

- [ ] **Step 2: Replace `<!-- HERO: Task 3 -->` with hero HTML**

```html
<div class="hero">
  <div class="terminal">
    <div class="terminal-bar">
      <span class="dot dot-red"></span>
      <span class="dot dot-yellow"></span>
      <span class="dot dot-green-dot"></span>
      <span class="terminal-title">bash &#8212; ~/portfolio</span>
    </div>
    <div class="terminal-body" id="terminal-body">
      <div>
        <span class="t-prompt">&#10095; </span><span class="t-cmd">whoami</span>
      </div>
      <div class="t-block">
        <div><span class="t-key">name</span>: <span class="t-val">"Yulei Liu"</span></div>
        <div><span class="t-key">role</span>: <span class="t-val">"DevSecOps &amp; Cloud Infrastructure Professional"</span></div>
        <div><span class="t-key">location</span>: <span class="t-val">"Sydney, NSW, Australia"</span></div>
        <div><span class="t-key">employers</span>: <span class="t-val">["HashiCorp", "AppDynamics", "IBM"]</span></div>
      </div>
      <div style="margin-top:8px;">
        <span class="t-prompt">&#10095; </span><span class="t-cmd">skills --list</span>
      </div>
      <div class="t-block">
        <div><span class="t-key">iac</span>:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <span class="t-val">["Terraform", "HCL", "Sentinel Policies"]</span></div>
        <div><span class="t-key">security</span>: <span class="t-val">["Vault", "TPM 2.0", "OIDC", "JWT", "SPIFFE", "mTLS"]</span></div>
        <div><span class="t-key">languages</span>:<span class="t-val"> ["Go", "Python", "Shell"]</span></div>
        <div><span class="t-key">platform</span>: <span class="t-val">["Docker", "Kong Gateway", "Bitbucket Pipelines"]</span></div>
      </div>
      <div style="margin-top:8px;">
        <span class="t-prompt">&#10095; </span><span class="cursor"></span>
      </div>
    </div>
  </div>
  <div class="hero-cta">
    <a href="#projects" class="btn-primary">View Projects</a>
    <a href="https://github.com/ausmartway" class="btn-ghost" target="_blank" rel="noopener">GitHub Profile</a>
    <a href="https://linkedin.com/in/yulei-liu" class="btn-ghost" target="_blank" rel="noopener">LinkedIn</a>
  </div>
</div>
```

- [ ] **Step 3: Verify hero renders correctly**

Expected: macOS window chrome (3 dots), title "bash — ~/portfolio", all terminal content visible with correct syntax colors. Three CTA buttons below. On mobile (390px): terminal body scrolls horizontally.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add terminal hero static structure"
```

---

## Task 4: Typewriter Animation

**Files:**
- Modify: `index.html` (script block only)

Clears the terminal body on load and rebuilds content progressively using safe DOM methods (no innerHTML — all text set via textContent or element construction).

- [ ] **Step 1: Replace the `<script>` block content with hamburger JS + typewriter JS**

Keep the hamburger IIFE from Task 2, then append this typewriter IIFE after it:

```js
(function () {
  var body = document.getElementById('terminal-body');
  if (!body) return;

  // Clear static content — will be rebuilt by animation
  while (body.firstChild) body.removeChild(body.firstChild);

  function delay(ms) {
    return new Promise(function (resolve) { setTimeout(resolve, ms); });
  }

  function makeSpan(cls, text) {
    var el = document.createElement('span');
    el.className = cls;
    if (text !== undefined) el.textContent = text;
    return el;
  }

  function makeDiv(children, style) {
    var el = document.createElement('div');
    if (style) el.setAttribute('style', style);
    children.forEach(function (c) { el.appendChild(c); });
    return el;
  }

  function makeText(text) {
    return document.createTextNode(text);
  }

  async function typeInto(el, text, msPerChar) {
    for (var i = 0; i < text.length; i++) {
      el.textContent += text[i];
      await delay(msPerChar);
    }
  }

  function appendWhoamiOutput() {
    var block = document.createElement('div');
    block.className = 't-block';

    var rows = [
      [makeSpan('t-key', 'name'),      makeText(': '), makeSpan('t-val', '"Yulei Liu"')],
      [makeSpan('t-key', 'role'),      makeText(': '), makeSpan('t-val', '"DevSecOps & Cloud Infrastructure Professional"')],
      [makeSpan('t-key', 'location'), makeText(': '), makeSpan('t-val', '"Sydney, NSW, Australia"')],
      [makeSpan('t-key', 'employers'),makeText(': '), makeSpan('t-val', '["HashiCorp", "AppDynamics", "IBM"]')],
    ];
    rows.forEach(function (children) { block.appendChild(makeDiv(children)); });
    body.appendChild(block);
  }

  function appendSkillsOutput() {
    var block = document.createElement('div');
    block.className = 't-block';

    var rows = [
      [makeSpan('t-key', 'iac'),       makeText(':      '), makeSpan('t-val', '["Terraform", "HCL", "Sentinel Policies"]')],
      [makeSpan('t-key', 'security'),  makeText(': '),      makeSpan('t-val', '["Vault", "TPM 2.0", "OIDC", "JWT", "SPIFFE", "mTLS"]')],
      [makeSpan('t-key', 'languages'), makeText(':'),       makeSpan('t-val', ' ["Go", "Python", "Shell"]')],
      [makeSpan('t-key', 'platform'),  makeText(': '),      makeSpan('t-val', '["Docker", "Kong Gateway", "Bitbucket Pipelines"]')],
    ];
    rows.forEach(function (children) { block.appendChild(makeDiv(children)); });
    body.appendChild(block);
  }

  async function run() {
    // Step 1: prompt + type "whoami"
    var cmd1 = makeSpan('t-cmd', '');
    body.appendChild(makeDiv([makeSpan('t-prompt', '\u276f '), cmd1]));
    await typeInto(cmd1, 'whoami', 40);

    // Step 2: pause, show whoami output
    await delay(200);
    appendWhoamiOutput();

    // Step 3: pause, prompt + type "skills --list"
    await delay(400);
    var cmd2 = makeSpan('t-cmd', '');
    body.appendChild(makeDiv([makeSpan('t-prompt', '\u276f '), cmd2], 'margin-top:8px'));
    await typeInto(cmd2, 'skills --list', 40);

    // Step 4: pause, show skills output
    await delay(200);
    appendSkillsOutput();

    // Step 5: pause, final prompt + blinking cursor
    await delay(300);
    var cursor = document.createElement('span');
    cursor.className = 'cursor';
    body.appendChild(makeDiv([makeSpan('t-prompt', '\u276f '), cursor], 'margin-top:8px'));
  }

  run();
}());
```

- [ ] **Step 2: Verify animation sequence**

Reload page. Confirm:
1. Terminal body starts empty
2. `❯ ` appears, `whoami` types out (~7 chars × 40ms = ~280ms)
3. Pause, then 4 whoami output lines appear simultaneously
4. Longer pause, `❯ ` + `skills --list` types out
5. Pause, 4 skills lines appear
6. Short pause, final `❯ █` with blinking cursor

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add typewriter animation to terminal hero"
```

---

## Task 5: Expertise Grid

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add expertise CSS inside `<style>` block**

```css
/* ── Expertise Grid ── */
.tech-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 12px;
}
.tech-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 14px 16px;
  transition: border-color 0.2s;
}
.tech-card:hover { border-color: var(--blue); }
.tech-card-label {
  font-family: 'JetBrains Mono', monospace;
  font-size: 11px;
  color: var(--muted);
  letter-spacing: 0.06em;
  text-transform: uppercase;
  margin-bottom: 6px;
}
.tech-card-name {
  font-size: 14px;
  font-weight: 600;
  color: var(--text);
  margin-bottom: 4px;
}
.tech-card-items {
  font-size: 12px;
  color: var(--muted);
  line-height: 1.5;
}

@media (max-width: 600px) {
  .tech-grid { grid-template-columns: repeat(2, 1fr); }
}
```

- [ ] **Step 2: Replace `<!-- EXPERTISE: Task 5 -->` with the expertise section**

```html
<section id="expertise" class="section">
  <div class="section-label">// expertise</div>
  <div class="section-title">Core Technologies &amp; Tools</div>
  <div class="tech-grid">
    <div class="tech-card">
      <div class="tech-card-label">HashiCorp Suite</div>
      <div class="tech-card-name">Infrastructure &amp; Secrets</div>
      <div class="tech-card-items">Terraform Cloud/Enterprise &middot; Vault &middot; HCL &middot; Sentinel</div>
    </div>
    <div class="tech-card">
      <div class="tech-card-label">Security</div>
      <div class="tech-card-name">Zero-Trust &amp; AuthN</div>
      <div class="tech-card-items">TPM 2.0 &middot; OIDC &middot; JWT &middot; SPIFFE &middot; OpenSSL &middot; mTLS</div>
    </div>
    <div class="tech-card">
      <div class="tech-card-label">Languages</div>
      <div class="tech-card-name">Programming</div>
      <div class="tech-card-items">Go &middot; Python &middot; HCL &middot; Shell Scripting</div>
    </div>
    <div class="tech-card">
      <div class="tech-card-label">Platform</div>
      <div class="tech-card-name">CI/CD &amp; DevOps</div>
      <div class="tech-card-items">Bitbucket Pipelines &middot; Docker &middot; Kong Gateway</div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Verify expertise section**

Expected: 4 cards in a row on desktop. 2×2 grid on mobile. Card border turns blue on hover.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add expertise grid section"
```

---

## Task 6: Featured Projects

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add projects CSS inside `<style>` block**

```css
/* ── Projects ── */
.project-category { margin-bottom: 36px; }

.cat-badge {
  font-family: 'JetBrains Mono', monospace;
  font-size: 12px;
  font-weight: 600;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  padding: 4px 10px;
  border-radius: 4px;
  display: inline-block;
  margin-bottom: 14px;
}
.cat-infra    { color: #58a6ff; background: rgba(88,166,255,0.1);  border: 1px solid rgba(88,166,255,0.3);  }
.cat-security { color: #f78166; background: rgba(247,129,102,0.1); border: 1px solid rgba(247,129,102,0.3); }
.cat-auth     { color: #d2a8ff; background: rgba(210,168,255,0.1); border: 1px solid rgba(210,168,255,0.3); }

.project-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(340px, 1fr));
  gap: 14px;
}
.project-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 18px 20px;
  text-decoration: none;
  display: block;
  transition: border-color 0.2s, transform 0.2s;
}
.project-card:hover {
  border-color: var(--blue);
  transform: translateY(-2px);
}
.project-name {
  font-family: 'JetBrains Mono', monospace;
  font-size: 15px;
  font-weight: 600;
  color: var(--blue);
  margin-bottom: 8px;
}
.project-desc {
  font-size: 13px;
  color: var(--muted);
  line-height: 1.55;
  margin-bottom: 14px;
}
.project-meta {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  align-items: center;
}

@media (max-width: 600px) {
  .project-grid { grid-template-columns: 1fr; }
}
```

- [ ] **Step 2: Replace `<!-- PROJECTS: Task 6 -->` with projects HTML**

```html
<section id="projects" class="section">
  <div class="section-label">// projects</div>
  <div class="section-title">Featured Projects</div>

  <div class="project-category">
    <span class="cat-badge cat-infra">Infrastructure Management</span>
    <div class="project-grid">
      <a class="project-card" href="https://github.com/ausmartway/tfc-config-as-code" target="_blank" rel="noopener">
        <div class="project-name">tfc-config-as-code</div>
        <div class="project-desc">Manages Terraform Cloud configuration as code &mdash; workspaces, projects, teams, modules, and settings with modular IaC design.</div>
        <div class="project-meta">
          <span class="lang-badge">HCL</span>
          <span class="focus-tag">Terraform Cloud Config Management</span>
        </div>
      </a>
      <a class="project-card" href="https://github.com/ausmartway/vault-config-as-code" target="_blank" rel="noopener">
        <div class="project-name">vault-config-as-code</div>
        <div class="project-desc">Transforms Vault configuration into reproducible infrastructure code. Covers KV, Transit, PKI, Identity engines, and namespace management.</div>
        <div class="project-meta">
          <span class="lang-badge">HCL</span>
          <span class="lang-badge">Python</span>
          <span class="lang-badge">Shell</span>
          <span class="focus-tag">HashiCorp Vault Config</span>
        </div>
      </a>
    </div>
  </div>

  <div class="project-category">
    <span class="cat-badge cat-security">Security Tools</span>
    <div class="project-grid">
      <a class="project-card" href="https://github.com/ausmartway/tfcvar-sec" target="_blank" rel="noopener">
        <div class="project-name">tfcvar-sec</div>
        <div class="project-desc">CLI tool that scans TFC/TFE variables to detect exposed secrets not marked as sensitive. Available via Homebrew, curl, or Docker.</div>
        <div class="project-meta">
          <span class="lang-badge">Go</span>
          <span class="focus-tag">Terraform Security Scanning</span>
        </div>
      </a>
      <a class="project-card" href="https://github.com/ausmartway/vault-tpm-helper" target="_blank" rel="noopener">
        <div class="project-name">vault-tpm-helper</div>
        <div class="project-desc">Solves "Secret Zero" using TPM 2.0 &mdash; authenticates to Vault with hardware-protected keys that never leave the chip. Supports vTPM too.</div>
        <div class="project-meta">
          <span class="lang-badge">Go</span>
          <span class="focus-tag">Hardware-Backed Authentication</span>
        </div>
      </a>
    </div>
  </div>

  <div class="project-category">
    <span class="cat-badge cat-auth">Authentication Solutions</span>
    <div class="project-grid">
      <a class="project-card" href="https://github.com/ausmartway/vault-identity-token-demo" target="_blank" rel="noopener">
        <div class="project-name">vault-identity-token-demo</div>
        <div class="project-desc">Zero-trust auth using Vault + Kong Gateway. Centralized JWT tokens, SPIFFE workload identity, department/role-based access control.</div>
        <div class="project-meta">
          <span class="lang-badge">Shell</span>
          <span class="focus-tag">Zero-Trust Architecture</span>
        </div>
      </a>
      <a class="project-card" href="https://github.com/ausmartway/bitbucket-pipeline-oidc-with-vault" target="_blank" rel="noopener">
        <div class="project-name">bitbucket-pipeline-oidc-with-vault</div>
        <div class="project-desc">Reference impl for secretless CI/CD using native OIDC token auth to Vault. Eliminates hardcoded secrets across Bitbucket repos.</div>
        <div class="project-meta">
          <span class="lang-badge">HCL</span>
          <span class="focus-tag">CI/CD Secrets Management</span>
        </div>
      </a>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Verify projects section**

Expected: 3 category badges (blue/orange/purple), 2-column grids on desktop, 1-column on mobile. Hover lifts card 2px and turns border blue. All 6 GitHub links correct.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add featured projects section with category grids"
```

---

## Task 7: Contact Section + Footer

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add contact + footer CSS inside `<style>` block**

```css
/* ── Contact ── */
.contact-body {
  color: var(--muted);
  max-width: 520px;
  margin-bottom: 20px;
}
.contact-links {
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
}

/* ── Footer ── */
footer {
  border-top: 1px solid var(--border);
  padding: 28px 32px;
  text-align: center;
  font-family: 'JetBrains Mono', monospace;
  font-size: 12px;
  color: var(--muted);
}
footer a {
  color: var(--blue);
  text-decoration: none;
}
footer a:hover { text-decoration: underline; }
.footer-brand { color: var(--green); }
```

- [ ] **Step 2: Replace `<!-- CONTACT+FOOTER: Task 7 -->` with HTML**

```html
<section id="contact" class="section">
  <div class="section-label">// contact</div>
  <div class="section-title">Get In Touch</div>
  <p class="contact-body">Open to collaborating on DevSecOps, cloud infrastructure, and HashiCorp ecosystem projects.</p>
  <div class="contact-links">
    <a href="https://github.com/ausmartway" class="btn-ghost" target="_blank" rel="noopener">GitHub &#8594;</a>
    <a href="https://linkedin.com/in/yulei-liu" class="btn-ghost" target="_blank" rel="noopener">LinkedIn &#8594;</a>
    <a href="mailto:yulei.liu@gmail.com" class="btn-ghost">Email &#8594;</a>
  </div>
</section>

<footer>
  <span class="footer-brand">~/yuleiliu</span> &middot;
  <a href="https://github.com/ausmartway" target="_blank" rel="noopener">github.com/ausmartway</a> &middot;
  Sydney, NSW, Australia
</footer>
```

- [ ] **Step 3: Verify contact + footer**

Expected: section label, title, muted body text, 3 ghost buttons in a row. Footer with green `~/yuleiliu`, blue GitHub link, muted location text.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add contact section and footer"
```

---

## Task 8: Full-Page Visual Verification

**Files:**
- Read-only verification (edit `index.html` only if issues found)

- [ ] **Step 1: Desktop screenshot at 1280px**

Navigate to the local file. Take a full-page screenshot. Verify all sections render correctly against the mockup at `.superpowers/brainstorm/64667-1774125386/full-mockup.html`.

- [ ] **Step 2: Mobile screenshot at 390px**

Resize to 390×844. Verify:
- ☰ hamburger visible, nav links hidden
- Terminal scrolls horizontally (no overflow)
- Expertise: 2-column grid
- Projects: 1-column grid
- CTA + contact buttons wrap

- [ ] **Step 3: Fix any regressions and commit**

```bash
git add index.html
git commit -m "fix: responsive and visual polish after full review"
```

---

## Task 9: Push to GitHub Pages

- [ ] **Step 1: Confirm clean state**

```bash
git status
```

Expected: nothing to commit.

- [ ] **Step 2: Push**

```bash
git push origin master
```

- [ ] **Step 3: Verify live site**

Wait ~60 seconds. Open `https://ausmartway.github.io/` and confirm the new design is live.
