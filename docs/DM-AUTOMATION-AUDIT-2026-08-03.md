# DM Automation & Lead Magnet Delivery — Read-Only Audit

**Date:** 2026-08-03
**Scope:** TikTok · Instagram · Facebook · ManyChat · n8n · Google Drive · Stan Store · landing pages
**Method:** read-only. No workflow, message, link, or file was modified.
**Systems reached:** n8n Cloud (`wilkinsrealty.app.n8n.cloud`, 65 workflows, 14 data tables), GitHub (`Driven99/strategic-acquisition-landing`, `Driven99/lumenholdingsllc.github.io`, `Driven99/wilkins-dynasty`).

---

## 1. Executive Summary

**There is exactly one keyword trigger in the entire system: `RISE`. It is live on three platforms. It delivers nothing.**

The funnel is a three-stage chain, and it is broken at every stage after the first:

| Stage | Component | State |
|---|---|---|
| 1. Demand creation | Clip Factory mints "Comment RISE" into **every** caption, posts to IG + TikTok + FB 3×/day | ✅ **Working** |
| 2. Comment reply | ManyChat `Auto-DM links from comments` (live) / TRR Comment Brain (active) | ⚠️ **Live but 0 real runs** |
| 3. Asset delivery | — | ❌ **Does not exist** |

The single most important finding: **no lead magnet file exists anywhere.** I searched every n8n workflow node, all 14 n8n data tables, and all three repositories for `.pdf`, `.zip`, `.docx`, `drive.google.com`, download URLs, and asset references. There is no PDF, no Google Drive file, no hosted download, and no data table tracking delivered assets. The captions going out right now on three platforms promise "Comment RISE and I'll send you the full breakdown" — and there is no breakdown to send.

Three further structural problems:

- **The reply bot is a dead end by design.** TRR Comment Brain rule #4 instructs it: *if the comment contains RISE, tell them to check their DMs.* The workflow has no DM-sending node. It writes a comment promising a DM that its own architecture cannot send.
- **Three overlapping comment responders exist** (ManyChat AI, TRR Comment Brain, IG COMMENT RESPONDER). Your own engineering notes carry an explicit warning: *"Never run both as comment responders at once — a single comment would get two public replies."*
- **A paid clock is running.** ManyChat Pro auto-converts to **$39/mo (~$468/yr) around 2026-08-11** for a flow that has recorded **0 runs**. That date is flagged UNVERIFIED in your own notes.

**Sequencing note:** your notes correctly observe that @think.rise.repeat is at ~11 followers, so the funnel sits downstream of distribution that doesn't exist yet. That does not reduce the urgency of building the asset — it means the asset can be built calmly and correctly *before* volume arrives, rather than under pressure. But it does mean the ManyChat spend is currently buying capacity you cannot yet use.

---

## 2. Master Inventory

### 2.1 Keyword triggers

| Platform | Keyword | Trigger | DM Message | Asset Sent | File Name | Storage Location | URL | Status | Notes |
|---|---|---|---|---|---|---|---|---|---|
| Instagram | **RISE** | Comment on any post containing "RISE" | ManyChat `Auto-DM links from comments` — **exact copy not readable from this session** | **None** | — | — | — | 🔴 **Broken — no asset** | Flow is LIVE with **0 runs** as of 2026-07-30 audit |
| Instagram | **RISE** | Same comment, parallel path | TRR Comment Brain posts a *public comment reply* saying to check DMs | **None** | — | — | — | 🔴 **Broken — promises undeliverable DM** | Workflow `WGIMV0kPyUseEn4K`, active; has no DM node |
| TikTok | **RISE** | Caption says "Comment RISE" | **No automation exists** | **None** | — | — | — | 🔴 **Dead trigger** | Comment automation deliberately rejected (ToS/ban risk) — see §6 |
| Facebook | **RISE** | Caption says "Comment RISE" | **No automation exists** | **None** | — | — | — | 🔴 **Dead trigger** | No FB comment responder built |

**No other keyword exists.** START, AI, GUIDE, MAMBA, MATH, WIN — none are present in any workflow, caption rule, or data table. The Clip Factory content agent explicitly forbids inventing alternates:

> *"NEVER invent any other trigger word or emoji-drop CTA (no MAMBA, no MATH, no WIN, no 'drop a 🔥')."*
> — `Dynasty Clip Factory` → node **Hooks and Angles Agent**, SEO rule 4

### 2.2 Publishing automations (the demand side — this half works)

| Platform | Workflow | Node | Account ID | Caption transform | Status |
|---|---|---|---|---|---|
| Instagram | `Dynasty Clip Factory — Reel-to-Riches Engine` (`uMaOIQgk6Mk2fqkN`) | Publish Drip Clip | `dml6YXJkLTQtMTkzNTY5LTI0NDAw` | Appends `🏛️ Structure & credit game: @themonetizedvault` | 🟢 Active |
| TikTok | same | Publish Drip Clip TikTok | `dml6YXJkLTItMTk0NTI3` | Rewrites `@think.rise.repeat` → `@thinkriserepeat` | 🟢 Active |
| Facebook | same | Publish Drip Clip Facebook | `dml6YXJkLTMtMTk0NzU4LTI0NzQz` | Rewrites `@think.rise.repeat` → `@thinkriserepeat` | 🟢 Active |

All three publish via Vizard (`elb-api.vizard.ai/.../publish-video`). Vizard holds the Meta OAuth — n8n has no Meta credential. Schedule: 6:00 AM / 12:00 PM / 7:00 PM ET.

### 2.3 Comment-response automations

| Name | ID | Platform | Live? | What it sends | Evidence of real use |
|---|---|---|---|---|---|
| TRR Comment Brain — DeepSeek Reply Engine | `WGIMV0kPyUseEn4K` | any (param) | 🟢 active | Public comment reply, ≤200 chars, DeepSeek v4-flash | **6 executions ever** (5 success, 1 error), last 2026-07-31. Your notes: *"nothing calls it… all manual tests."* |
| IG COMMENT RESPONDER | `8C6IOitQnFAzRT3g` | Instagram | 🔴 **inactive** | Public comment reply via Graph API | **0 trigger runs.** Blocked: literal placeholder `<__PLACEHOLDER_VALUE__…>` in "Get Recent Media"; no Meta credential on the instance |
| ManyChat `Auto-DM links from comments` | acct `fb5337740` | Instagram | 🟢 live | Auto-DM on RISE | **0 runs** as of 2026-07-30 |
| ManyChat — 2 × Untitled DRAFT | acct `fb5337740` | Instagram | 🔴 draft | Stock ManyChat placeholder copy | Created 07-29 & 07-30, both abandoned, never Set Live |

### 2.4 Landing pages / delivery destinations

| Destination | Source | Purpose | Asset | Status |
|---|---|---|---|---|
| `https://stan.store/Monetized-Vault` | `strategic-acquisition-landing/index.html:666` | Paid checkout, $97 (from $197) | "The Complete Corporation Acquisition Guide" | ⚠️ **Unverifiable** — network blocked (§7) |
| `https://lumenholdingsllc.com` | `lumenholdingsllc.github.io/CNAME` | Corporate site | None — Calendly + mailto + tel only | ⚠️ **Unverifiable** |
| `https://wilkinsrealty.app.n8n.cloud/form/biz-xray` | `BI ENGINE — Public Front Door` (`3GefyaVzjoY36bNM`) | Free AI Business X-Ray report | Generated HTML report (not a file) | 🟢 Active, live-tested 2026-07-24 |
| `https://wilkinsrealty.app.n8n.cloud/form/buyers` | `Cash Buyer Opt-In` (`GkaLlx6q1aQXVla6`) | Buyer list capture | None | 🟢 Active |

---

## 3. Every File Currently Being Delivered

**None.**

This is a complete answer, not an incomplete search. Verified by:
- Every node parameter across the DM/content workflows — no file, URL, or attachment node.
- All 14 n8n data tables — no asset, magnet, delivery, or subscriber table exists.
- `grep` for `.pdf|.zip|.docx|.epub|drive.google|download` across all three repos — zero lead-magnet hits.

The only user-facing artifacts the system produces at all are the **AI Business X-Ray report** (rendered HTML on a form completion page, logged to `xray_reports`) and the **published video clips** themselves. Neither is the promised RISE payoff.

---

## 4. Lead Magnets That Exist But Are Not Used

Assets referenced in your records but wired to **nothing**:

| Asset | Location | Why it's unused |
|---|---|---|
| `Fabulous-Five-Wealth-Blueprint.pdf` | `C:\Users\bigwi\fabulous-five\` (local Windows) | Different brand (Fabulous Five, not TRR). Not hosted, not public, not referenced by any automation. |
| `Deal-Analyzer.xlsx` + Blueprint `.docx` | `D:\Claude Coding\fabulous-five\` | **D: drive was disconnected/offline as of 2026-07-07.** Existence unconfirmed since. |
| "The Complete Corporation Acquisition Guide" | Sold via Stan Store | Paid product ($97), not a lead magnet. **No file present in the repo** — the landing page's cover is an inline SVG placeholder, not a real cover image. |
| `M1-DYNASTY-SCORE-SPEC.md` | `~/Downloads` only | Your own Phase-0 audit flags: *"Exists only in `~/Downloads`, not in any repo."* Internal spec, not customer-facing. |
| `dynasty-blueprint.html`, `dynasty-vault.html` | `wilkins-dynasty/` (private repo) | Internal system maps. Not published, not branded for delivery. |
| AI Business X-Ray | `3GefyaVzjoY36bNM` | **Best consolidation candidate** — see §8. Live, free, zero-credential, already proven. Currently has no connection to the RISE funnel. |

---

## 5. Automations With Missing or Broken Assets

| # | Automation | Defect | Impact |
|---|---|---|---|
| 1 | ManyChat `Auto-DM links from comments` | Live, 0 runs, **no asset to send** | Every RISE commenter gets nothing |
| 2 | TRR Comment Brain `WGIMV0kPyUseEn4K` | Rule 4 promises "check your DMs"; workflow has **no DM node** | Public promise the system cannot keep |
| 3 | TRR Comment Brain — webhook URL | n8n's published Production URL **404s**. Only `https://wilkinsrealty.app.n8n.cloud/webhook/trr-comment-brain` (short form) resolves | Wiring ManyChat to the published URL would silently 404 every comment forever. **The dead form was recorded in SESSION_HANDOFF 2026-07-28** — verify before any integration |
| 4 | IG COMMENT RESPONDER `8C6IOitQnFAzRT3g` | Inactive; literal placeholder for IG Business account ID; **no Meta credential exists** among the instance's credentials | Free replacement for ManyChat is unavailable |
| 5 | Meta Graph API app "Dynasty HQ" | Half-created; wizard died at password confirmation (automated browser treated as unrecognized device) | Blocks #4. Your notes are explicit this **cannot** be finished from an automated browser — needs ~60s in a trusted everyday browser |
| 6 | ManyChat — 2 abandoned DRAFT flows | Stock placeholder copy, never Set Live | Clutter; the 07-30 draft has the correct skeleton and is worth salvaging or deleting, not leaving |
| 7 | `ig_replied_comments` table | Has a `media_id` column that `IG COMMENT RESPONDER` **never writes** | Schema drift; comments can't be traced to their post |
| 8 | Clip Factory publish chain | If Instagram succeeds but TikTok or Facebook fails, the retry **re-posts to Instagram** | Duplicate IG posts. Documented as "known residual" in the Drip Status sticky note; needs per-platform status columns |
| 9 | `strategic-acquisition-landing` | Repo description says **"Foundations of Strategic Acquisition"**; page title says **"The Complete Corporation Acquisition Guide"** | Product-name collision across your own surfaces |

---

## 6. Gap Analysis

**Keywords that send nothing:** RISE — on all three platforms. That is 100% of your keyword inventory.

**Keywords pointing to missing files:** RISE. The file has never existed; this is not a broken link, it is an unbuilt asset.

**Broken URLs:** the n8n-published Production URL for `trr-comment-brain` (404s while reporting `active: true`). No other broken URL confirmed — see §7 for what could not be tested.

**Duplicate automations / lead magnets:**
- **Three comment responders** for one Instagram account (ManyChat AI, TRR Comment Brain, IG COMMENT RESPONDER). Your own note: *"Never run both as comment responders at once — a single comment would get two public replies."* This is a live double-reply risk the moment two go active together.
- Four near-identical `AI Ad Production Pipeline` workflows (`T633yw0HoJkbcWKA`, `78JwWeDHYrzrib6t`, `Esm6fmQaQfLcORkR`, `Y7NL9REaKncdraIu`) — only the last is active.
- Two `Workflow 7 — Auto Sequence Runner` variants (`oSGNMOYfsOcR9ifL`, `dVaU7ftyCvRNs5nX`), both inactive.

**Outdated PDFs:** none in service (none exist). The nearest artifacts — the Fabulous Five blueprint and Deal Analyzer — are on local/offline drives with unverified currency.

**Missing branding:**
- **Handle inconsistency by platform.** IG captions use `@think.rise.repeat`; TikTok and Facebook get an automated rewrite to `@thinkriserepeat`. A viewer moving between platforms sees two different handles.
- **Second brand injected on Instagram only.** IG posts append `🏛️ Structure & credit game: @themonetizedvault`. TikTok and FB do not. One brand's audience is being split across two handles inconsistently. Note: your Clip Factory memory carries a sovereign-citizen-adjacent caution regarding `@themonetizedvault` content — worth a compliance read before scaling that cross-promo.
- **No branded asset template exists at all**, because no asset exists.
- Landing page cover art is a generated SVG placeholder reading "2025 Edition • 120+ Pages" — a **2025** edition marker on a page that hasn't been touched since 2025-08-24.

**Conversion opportunities:**
- Captions carry both a RISE trigger *and* a low-effort question *and* a follow CTA *and* an open loop. That is four asks per caption. Dropping one would sharpen the RISE conversion.
- `Comment RISE` fires on **every** caption regardless of clip topic — one generic promise ("the full breakdown") against wildly varying content. Topic-matched payoffs convert materially better.
- The X-Ray form captures an email but is not connected to the social funnel at all.

---

## 7. Evidence Gaps — What I Could NOT Verify

Stated explicitly rather than guessed, per your constraint:

| # | Unverifiable | Why | How to close it |
|---|---|---|---|
| 1 | **Whether any URL actually resolves** — `stan.store/Monetized-Vault`, `lumenholdingsllc.com`, all n8n webhooks | This environment's network policy returned **403 on CONNECT** for every outbound host. Both `curl` and WebFetch blocked. **Zero live link checks were possible.** | Run the checks from an unrestricted machine |
| 2 | **Exact ManyChat DM copy, flow logic, and current live/draft state** | No ManyChat MCP connector or API access in this session. All ManyChat facts here come from your own audit note dated **2026-07-30** — four days stale | Open ManyChat → Automation, or connect its API |
| 3 | **Google Drive contents** | The Google Drive connector is installed and authenticated but **`enabledInChat: false`** — toggled off for this session | Enable Google Drive in this chat's connector settings and re-run |
| 4 | **TikTok / Instagram / Facebook native automation settings** | No platform API access. Only the n8n and Vizard side is visible | Check each platform's native tools directly |
| 5 | **Whether the 6 Comment Brain executions were ManyChat or manual** | The n8n API returned execution metadata but no node-level payload | Inspect the executions in the n8n UI |
| 6 | **ManyChat trial end date (~2026-08-11) and the $39/mo price** | Your note flags the date UNVERIFIED (Settings → Subscriptions is JS-routed and wouldn't open). Pricing has been quoted wrong **twice** before | Confirm on ManyChat's billing screen before the keep/cancel call |
| 7 | **Local Windows assets** (`Fabulous-Five-Wealth-Blueprint.pdf`, `Deal-Analyzer.xlsx`) | Not reachable from this Linux container. D: was offline as of 2026-07-07 | Check the drives directly |
| 8 | Whether GitHub Pages actually serves either public repo | Both have `has_pages: true`, but page serving couldn't be fetched | Load the URLs from an unrestricted browser |

**One correction to your own records:** `meta-graph-api-blocker.md` states IG COMMENT RESPONDER's model is `deepseek-chat` and "must move to `deepseek-v4-flash` first." The live workflow now reads `deepseek-v4-flash` on both the primary and Gemini fallback models. That migration is **already done** — the note is stale.

---

## 8. Recommendations — Consolidating Into One Lead Magnet Library

### Priority 0 — Stop the bleeding (this week)

1. **Decide the ManyChat question before ~2026-08-11.** A flow with 0 runs is auto-converting to ~$468/yr. Verify the real date and price in the billing UI first. Given that IG COMMENT RESPONDER is a built, free replacement blocked only on a ~60-second browser task, the honest reading is that ManyChat is buying capacity you cannot currently use.
2. **Either build the RISE asset or change the captions.** Right now every post on three platforms makes a promise the system cannot keep. Those are the two options; leaving it as-is is the only one that costs trust.
3. **Never activate two comment responders simultaneously.** Pick one owner per platform and write it down.

### Priority 1 — Build the asset (the actual unblock)

Ship **one** magnet, not a library-of-one-day. The fastest credible option already exists: the **AI Business X-Ray** (`3GefyaVzjoY36bNM`) is live, free to run, needs zero credentials, and is proven end-to-end. Wiring RISE → X-Ray form link gives you a real, differentiated payoff without authoring a PDF.

If you want a document instead, scope it to one topic that matches your highest-`ViralScore` clips rather than a generic "full breakdown."

### Priority 2 — Standing library structure

Do not scatter assets across `C:\`, `D:\`, Downloads, and Drive again. One home, one convention:

```
Google Drive / Lead Magnets/
  ├─ _LIVE/          ← only files currently being delivered
  ├─ _ARCHIVE/       ← superseded versions, never deleted
  └─ _SOURCE/        ← editable originals (Docs, Canva, .docx)
```

**Naming:** `TRR_<KEYWORD>_<AssetName>_v<N>_<YYYY-MM-DD>.pdf`
→ `TRR_RISE_WealthBlueprint_v1_2026-08-10.pdf`

The keyword is in the filename, so any file traces back to the automation that sends it — the exact traceability that is missing today.

**Version control:** bump `v<N>` on every content change. Never overwrite a live file in place — a stale cached CDN copy is indistinguishable from a working one. Move the old version to `_ARCHIVE/` and repoint the automation.

**Registry:** add an n8n data table `lead_magnets` with columns `keyword · platform · asset_name · file_id · public_url · version · status · last_verified · owner_workflow`. This is the single artifact whose absence made this audit hard — with it, this whole report becomes a query.

**Delivery link:** never hand a raw Drive URL to a DM flow. Use one stable redirect per keyword (`trr.link/rise` or an n8n webhook 302) so you can swap the underlying file without touching any automation.

### Priority 3 — Hygiene

- Archive the 3 dead `AI Ad Production Pipeline` variants and both `Workflow 7` variants.
- Delete or finish the 2 abandoned ManyChat drafts.
- Reconcile the handle split: standardize on one handle string, or accept the rewrite deliberately and document why.
- Add per-platform status columns to the Clip Factory ledger to close the duplicate-IG-post gap (defect #8).
- Add `media_id` writes to `IG COMMENT RESPONDER` so replies trace to posts (defect #7).
- **Add a link-check job.** A weekly workflow that HEADs every `public_url` in `lead_magnets` and posts failures to `#jarvis` would have caught the 404 webhook before it was recorded in a handoff doc.

### Priority 4 — Conversion

- Cut one of the four caption asks; test RISE-only against the current four-ask version.
- Topic-match the RISE payoff to the clip instead of a universal "full breakdown."
- Once an asset exists, capture email at delivery — the funnel currently builds no owned list on any platform.

---

## Appendix — Source Trace

| Finding | Source |
|---|---|
| RISE is the only keyword; alternates forbidden | `Dynasty Clip Factory` (`uMaOIQgk6Mk2fqkN`) → node **Hooks and Angles Agent**, SEO rule 4 |
| "check your DMs" instruction | `TRR Comment Brain` (`WGIMV0kPyUseEn4K`) → node **TRR Reply Agent**, rule 4 |
| Publish targets + account IDs | `uMaOIQgk6Mk2fqkN` → **Publish Drip Clip** / **…TikTok** / **…Facebook** |
| Duplicate-IG-post residual | `uMaOIQgk6Mk2fqkN` → **Sticky Note Drip Status** |
| ManyChat 0 runs, 2 drafts, trial date | `wilkins-dynasty/memory/manychat-trial-audit.md` |
| Webhook 404 gotcha; "nothing calls it" | `wilkins-dynasty/memory/trr-comment-brain.md` |
| Meta app half-created; no Meta credential | `wilkins-dynasty/memory/meta-graph-api-blocker.md` |
| Local PDFs / offline D: drive | `wilkins-dynasty/memory/fabulous-five-hq.md` |
| X-Ray engine live, zero-credential | `wilkins-dynasty/memory/monetized-vault-bi-engine.md` |
| Stan Store CTA, $97 price | `strategic-acquisition-landing/index.html:666` |
| `lumenholdingsllc.com` domain | `lumenholdingsllc.github.io/CNAME` |
| Comment Brain execution history (6) | n8n API `search_executions`, workflow `WGIMV0kPyUseEn4K` |
| No asset/magnet data table | n8n API `search_data_tables` — all 14 enumerated |
| Network 403s | `$HTTPS_PROXY/__agentproxy/status` → `recentRelayFailures` |
