# Website Modernization Design

**Date:** 2026-03-22
**Status:** Approved
**Scope:** Redesign `index.html` — enhanced standalone HTML, no Jekyll layout changes

---

## Goal

Modernize `ausmartway.github.io` to serve as a compelling personal brand/portfolio targeting hiring managers, recruiters, and technical clients in the DevSecOps space.

---

## Design Decisions

| Decision | Choice | Rationale |
|---|---|---|
| Implementation approach | Enhanced standalone `index.html` | Avoids Jekyll/GitHub Pages plugin risk; current file already bypasses Jekyll |
| Visual style | Dark & technical | Matches DevSecOps identity; signals "serious engineer" |
| Color palette | GitHub Dark | `#0d1117` base, `#58a6ff` blue, `#3fb950` green, `#30363d` border |
| Layout | Hero + card grid | Modern portfolio feel; projects scannable by category |
| Hero style | Terminal prompt | Distinctive, memorable, directly reinforces DevSecOps identity |
| Fonts | Inter (body) + JetBrains Mono (code/labels) via Google Fonts | Professional + technical; free, no build step |

---

## Architecture

Single file: `index.html` — self-contained with `<style>` and `<script>` blocks. No external dependencies beyond Google Fonts CDN. Fully GitHub Pages compatible.

---

## CSS Custom Properties

```css
--bg:      #0d1117
--surface: #161b22
--border:  #30363d
--text:    #e6edf3
--muted:   #8b949e
--blue:    #58a6ff
--green:   #3fb950
--orange:  #f78166
--purple:  #d2a8ff
--yellow:  #e3b341
```

---

## Shared Component Definitions

### Ghost Button
Border: `1px solid var(--border)`, background: `var(--surface)`, color: `var(--blue)`, padding: `9px 18px`, border-radius: `6px`, font-size: `14px`. Hover: border-color transitions to `var(--blue)`. Used in hero CTA and contact section.

### Focus Tag
Plain text label next to language badges. Font-size: `11px`, color: `var(--muted)`. No background or border. Example: "Terraform Cloud Config Management".

### Language Badge
Green pill: background `rgba(63,185,80,0.1)`, border `1px solid rgba(63,185,80,0.3)`, color `var(--green)`, font-family JetBrains Mono, font-size `11px`, padding `2px 8px`, border-radius `20px`.

---

## Sections

### 1. Sticky Navigation
- Brand (left): `~/yuleiliu` in `var(--green)` JetBrains Mono — this is the nav brand string
- Links (right): anchor links to in-page sections — `#expertise`, `#projects`, `#contact`. **Not** links to Jekyll pages (`about.md`, `projects.md`).
- Style: `position: sticky; top: 0; z-index: 100`, background `rgba(13,17,23,0.85)`, `-webkit-backdrop-filter: blur(12px); backdrop-filter: blur(12px)` (both prefixes for Safari compatibility), `border-bottom: 1px solid var(--border)`, height `56px`
- **Mobile (≤600px):**
  - Nav links hidden by default
  - Hamburger button (☰) shown at right, `font-size: 20px`, color `var(--muted)`
  - On click: toggles a full-width dropdown below the nav bar (not an overlay); dropdown has `background: var(--surface)`, `border-bottom: 1px solid var(--border)`, links stacked vertically with `padding: 12px 24px`
  - Dropdown dismissed by: clicking the ☰ again, clicking any nav link, or clicking anywhere outside the nav
  - Dropdown `z-index: 99` (below nav's 100 is wrong — use `z-index: 101` to sit above page content)
  - Implemented with a single vanilla JS toggle on the nav element's class

### 2. Terminal Hero
- macOS-style window chrome: red (`#ff5f57`) / yellow (`#febc2e`) / green (`#28c840`) dots, title `bash — ~/portfolio` centered in muted text
- Background `var(--surface)`, border `1px solid var(--border)`, border-radius `10px`, box-shadow `0 8px 32px rgba(0,0,0,0.4)`
- Terminal body font: JetBrains Mono 14px, line-height 1.9, padding `24px 28px 28px`
- `overflow-x: auto` on terminal body — content scrolls horizontally on narrow screens; minimum font-size stays at 14px (do not reduce)

**Typewriter animation sequence (vanilla JS):**
1. Page loads — terminal body is empty
2. Prompt `❯ ` appears instantly, then `whoami` types out at 40ms per character
3. After `whoami` finishes: 200ms pause, then all four output lines appear simultaneously (not typed)
4. 400ms pause, then prompt `❯ ` appears instantly, then `skills --list` types out at 40ms per character
5. After `skills --list` finishes: 200ms pause, then all four output lines appear simultaneously
6. 300ms pause, then final `❯ ` prompt appears with blinking cursor `█` on the same line — cursor is a `<span>` with CSS blink animation (`animation: blink 1s step-end infinite`)

**Syntax colors in output:**
- Keys (e.g. `name`, `role`): `var(--purple)`
- Values in quotes: `var(--orange)`
- Array brackets and commas: `var(--text)`
- Prompt `❯`: `var(--green)`
- Commands (`whoami`, `skills --list`): `var(--blue)`

**CTA buttons below terminal:**
- `View Projects` → `#projects` (primary: green filled, background `#238636`, border `1px solid #2ea043`)
- `GitHub Profile` → `https://github.com/ausmartway` (ghost button)
- `LinkedIn` → `https://linkedin.com/in/yulei-liu` (ghost button)

### 3. Expertise Grid
- Section label: `// expertise` — JetBrains Mono 12px, `var(--muted)`, letter-spacing `0.08em`, uppercase
- Section title: "Core Technologies & Tools" — Inter 22px bold, border-bottom `1px solid var(--border)`, margin-bottom `24px`
- Grid: `display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 12px`
- **Breakpoint override at ≤600px:** `grid-template-columns: repeat(2, 1fr)` — forces exactly 2 columns; removes the auto-fit minmax to avoid collision
- Cards: background `var(--surface)`, border `1px solid var(--border)`, border-radius `8px`, padding `14px 16px`, hover → `border-color: var(--blue)` with `transition: border-color 0.2s`

**4 cards:**
| Label | Name | Items |
|---|---|---|
| HASHICORP SUITE | Infrastructure & Secrets | Terraform Cloud/Enterprise · Vault · HCL · Sentinel |
| SECURITY | Zero-Trust & AuthN | TPM 2.0 · OIDC · JWT · SPIFFE · OpenSSL · mTLS |
| LANGUAGES | Programming | Go · Python · HCL · Shell Scripting |
| PLATFORM | CI/CD & DevOps | Bitbucket Pipelines · Docker · Kong Gateway |

### 4. Featured Projects
- Section label: `// projects`
- Section title: "Featured Projects"
- 3 category groups, each with a color-coded badge and a 2-column project grid

**Category badges:**
| Category | Text color | Background | Border |
|---|---|---|---|
| Infrastructure Management | `#58a6ff` | `rgba(88,166,255,0.1)` | `rgba(88,166,255,0.3)` |
| Security Tools | `#f78166` | `rgba(247,129,102,0.1)` | `rgba(247,129,102,0.3)` |
| Authentication Solutions | `#d2a8ff` | `rgba(210,168,255,0.1)` | `rgba(210,168,255,0.3)` |

Badge style: JetBrains Mono 12px, font-weight 600, letter-spacing 0.1em, uppercase, padding `4px 10px`, border-radius `4px`, `display: inline-block`, margin-bottom `14px`

**Project grid:** `display: grid; grid-template-columns: repeat(auto-fit, minmax(340px, 1fr)); gap: 14px`
**Mobile (≤600px):** `grid-template-columns: 1fr` — single column

**Project cards:** `<a>` tag, background `var(--surface)`, border `1px solid var(--border)`, border-radius `8px`, padding `18px 20px`, `text-decoration: none`. Hover: `border-color: var(--blue); transform: translateY(-2px)` with `transition: 0.2s`.

**Project data:**

*Infrastructure Management:*
- **tfc-config-as-code** | `https://github.com/ausmartway/tfc-config-as-code` | Manages Terraform Cloud configuration as code — workspaces, projects, teams, modules, and settings with modular IaC design. | Badges: `HCL` | Focus: Terraform Cloud Config Management
- **vault-config-as-code** | `https://github.com/ausmartway/vault-config-as-code` | Transforms Vault configuration into reproducible infrastructure code. Covers KV, Transit, PKI, Identity engines, and namespace management. | Badges: `HCL` `Python` `Shell` | Focus: HashiCorp Vault Config

*Security Tools:*
- **tfcvar-sec** | `https://github.com/ausmartway/tfcvar-sec` | CLI tool that scans TFC/TFE variables to detect exposed secrets not marked as sensitive. Available via Homebrew, curl, or Docker. | Badge: `Go` | Focus: Terraform Security Scanning
- **vault-tpm-helper** | `https://github.com/ausmartway/vault-tpm-helper` | Solves "Secret Zero" using TPM 2.0 — authenticates to Vault with hardware-protected keys that never leave the chip. Supports vTPM too. | Badge: `Go` | Focus: Hardware-Backed Authentication

*Authentication Solutions:*
- **vault-identity-token-demo** | `https://github.com/ausmartway/vault-identity-token-demo` | Zero-trust auth using Vault + Kong Gateway. Centralized JWT tokens, SPIFFE workload identity, department/role-based access control. | Badge: `Shell` | Focus: Zero-Trust Architecture
- **bitbucket-pipeline-oidc-with-vault** | `https://github.com/ausmartway/bitbucket-pipeline-oidc-with-vault` | Reference impl for secretless CI/CD using native OIDC token auth to Vault. Eliminates hardcoded secrets across Bitbucket repos. | Badge: `HCL` | Focus: CI/CD Secrets Management

### 5. Contact
- Section label: `// contact`
- Section title: "Get In Touch"
- Body text: "Open to collaborating on DevSecOps, cloud infrastructure, and HashiCorp ecosystem projects." — `var(--muted)`, max-width `520px`
- Three ghost buttons in a flex row (wrap on mobile to column):
  - `GitHub →` → `https://github.com/ausmartway`
  - `LinkedIn →` → `https://linkedin.com/in/yulei-liu`
  - `Email →` → `mailto:yulei.liu@gmail.com`

### 6. Footer
- `border-top: 1px solid var(--border)`, padding `28px 32px`, text-align center
- JetBrains Mono 12px, `var(--muted)`
- Content: `ausmartway · github.com/ausmartway · Sydney, NSW, Australia`
- `ausmartway` in `var(--green)`; `github.com/ausmartway` is a link in `var(--blue)` with hover underline
- Mobile: font-size stays 12px; wraps naturally

---

## Performance Notes

- Google Fonts loaded with `<link rel="preconnect" href="https://fonts.googleapis.com">` and `<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>` before the stylesheet link
- Font URL must include `&display=swap` to use `font-display: swap` and avoid render blocking

---

## Responsive Breakpoints

| Breakpoint | Behaviour |
|---|---|
| >1024px | Full desktop layout |
| 601px–1024px | Auto-fit grids reflow naturally; nav stays inline; no special overrides needed |
| ≤600px | Nav collapses to hamburger; expertise grid → 2 columns; project grid → 1 column; CTA buttons wrap |

---

## Mobile Behaviour Summary (≤600px)

| Element | Desktop | Mobile |
|---|---|---|
| Nav links | Inline right | Hidden; hamburger toggles full-width dropdown |
| Hero terminal | Full width | `overflow-x: auto`; font-size unchanged |
| Hero CTA buttons | Row | Flex-wrap; stack to column if needed |
| Expertise grid | 4 columns (auto-fit) | 2 columns (forced) |
| Project grid | 2 columns (auto-fit) | 1 column |
| Contact buttons | Row | Flex-wrap |
| Footer | Inline | Wraps naturally |
| Section titles | 22px | 18px |
| Section label | 12px | 12px (unchanged) |

---

## Constraints

- No JavaScript frameworks — vanilla JS only
- No Jekyll Liquid templates in `index.html` — served as static HTML; Jekyll ignores it
- No new files — all changes contained in `index.html`
- `_config.yml`, `_pages/`, `_projects/`, `about.md`, `projects.md` are untouched
- Google Fonts loaded via CDN with preconnect and `display=swap`

---

## Out of Scope

- Redesigning `about.md`, `projects.md`, `_pages/cv.md`
- Adding a blog, RSS feed, or search
- Dark/light mode toggle
- Animations beyond typewriter and hover transitions
- Favicon (separate task)
