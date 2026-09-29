# Enterprise templates · prototype v2

Native HTML/CSS/JS click-through for the n8n **Enterprise case-study** depth bet: private/golden company template library + hard rails (node allowlist, create-vs-copy). Replaces the screenshot+hotspot prototype in `../prototype/` (left intact as reference).

**Visual language:** n8n-like dark product shell. No PNG backgrounds. No Miro navy/yellow product theme. No Approved Stack light-paper look on product screens.

## Open

```bash
open "product work/enterprise templates solution/prototype-v2/index.html"
```

Or open `index.html` in any browser (file:// works; no build step).

## Roles (demo)

The demo map (`index.html`) groups screens by **job / role** (Miro Frame 5 swimlanes: Security → Admin → Builder → Member). Clicking a card sets that role before opening the screen. The primary path CTA still starts at Security → 00 allowlist; ProtoChrome **Back / Next** keeps journey order (not map section order). Product screens also show **Acting as …**; ProtoChrome keeps a compact **Acting as** dropdown to change persona mid-demo.

| Role | Job on the map | Screens |
|------|----------------|---------|
| **Security** | Define what builders may use · impact before block · notify owners | `00`, `00b`, `00c` |
| **Admin** | Assign create vs copy · library · approve | `01`, `01b`, `03b` |
| **Builder** | Build under rails · submit | `02`, `03`, `04` |
| **Member** | Copy / modify approved only (AI + MCP) | `05`, `06`, `08` + spurs `07`, `09` |

Role id is `member` (legacy `copy` migrates on load). State persists in `localStorage` (`ent-templates-v2-rebuild`). Use **Reset demo data** on the index map.

## Primary click path (~90s)

1. **00** Set approved capabilities — try **Block** on Slack (or stack prompt / SSH)
2. **00b** Review workflows that will break — impact count + owners → Confirm block
3. **00c** Notify owners of blocked capabilities — who was notified + sample copy
4. **01** Assign who can create vs copy templates — not a paywall
5. **01b** Turn on the company template library — Settings opt-in
6. **02** Build a workflow under policy rails — Submit menu; click a **Blocked** palette node → soft-block modal
7. **03** Submit a workflow as an internal template — ≠ Publish/Unpublish
8. **03b** Approve a pending internal template — Approve golden / Reject / Request changes
9. **05** Start from blank or company template (path switches to **Member**) — blank option gone
10. **06** Pick a golden template from the company library — Use a Golden card
11. **08** Open the workflow created from a golden template — **Provenance chip**

ProtoChrome **Back / Next** follows the full demo path including Browse workflows (04) and spurs.

## Secondary paths

- **AI climax:** from 05 or 06 → **07** Create a workflow from approved templates with AI (match + confirm + trust) → **08**
- **MCP echo:** **09** Prefer a golden template via MCP → **08** (same rails: golden prefer + allowlist refuse)

## Screen list

| File | Role section | Beat |
|------|--------------|------|
| `index.html` | — | Demo map by job / role + Start primary path |
| `screens/00-security-allowlist.html` | Security | Capability allowlist (tools + domains) |
| `screens/00b-block-impact-review.html` | Security | Impact review before block |
| `screens/00c-block-notify-owners.html` | Security | Notify workflow owners |
| `screens/01-admin-roles.html` | Admin | Create vs copy assignment |
| `screens/01b-library-enable.html` | Admin | Opt-in internal library |
| `screens/02-builder-editor.html` | Builder | Editor + allowlist palette |
| `screens/03-submit-as-template.html` | Builder | Submit ≠ publish |
| `screens/03b-approval-queue.html` | Admin | Pending / approve / reject |
| `screens/04-overview.html` | Builder | Workflow list → create |
| `screens/05-create-empty.html` | Member | Role-aware create |
| `screens/06-company-library.html` | Member | Internal SoR + card states |
| `screens/07-ai-assist.html` | Member (spur) | Approved match + confirm |
| `screens/08-result.html` | Member | Provenance chip |
| `screens/09-mcp.html` | Member (spur) | Optional MCP spur |

## Gaps this fills (vs v1 screenshots)

1. Security allowlist admin  
2. **Block impact review + owner notifications** (before / after disable)  
3. Admin enable internal library  
4. Real create vs copy roles (not upgrade CTA)  
5. Submit as internal ≠ Publish  
6. Approver queue  
7. Company library (not public Trending gallery)  
8. Card states: Draft / Pending / Golden / Archived  
9. Role chrome variants  
10. Result provenance chip  
11. AI assist with approved match + trust copy  
12. MCP vignette as same-rails echo  

## Architecture

See [`ARCHITECTURE.md`](ARCHITECTURE.md) for building blocks, `data-block` attributes, and how to move/change components.

## Hosted / local

- **Local:** `open "product work/enterprise templates solution/prototype-v2/index.html"` (or any static server).
- **Repo:** [BobMoonbird/enterprise-templates-proto](https://github.com/BobMoonbird/enterprise-templates-proto)
- **Live (GitHub Pages):** https://bobmoonbird.github.io/enterprise-templates-proto/
- Source of truth remains this folder; the GitHub repo is a publish mirror for hosting.

## Fake data

- `data/sample-templates.json` — golden / pending / archived / draft  
- `data/sample-nodes.json` — allowlisted + blocked nodes + role defs  
- Runtime copies live in `js/state.js` (loaded without fetch so `file://` works)
- `BLOCK_IMPACT` in `state.js` — fake workflows/owners for block review
