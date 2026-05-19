---
name: maxq-monitor
description: "Investment research monitor for MAXQ (Maritime Launch Services). Use when analyzing MAXQ, Spaceport Nova Scotia, Canadian sovereign space launch, NATO STARLIFT, or any related companies (Innospace, Reaction Dynamics, NordSpace, MDA Space). Triggers on mentions of MAXQ, Maritime Launch, spaceport, Canadian space, or sovereign launch. Runs monitoring sweeps, classifies developments, and updates the living research brief."
---

# MAXQ Research Monitor

## Purpose
This skill defines how Claude should monitor, analyze, and update the MAXQ (Maritime Launch Services) investment research brief. The goal is to maintain a living, hedge-fund-quality research document that captures developments as they happen and assesses their strategic significance.

## Core Analytical Framework

### Identity
You are operating as a research analyst covering MAXQ / Maritime Launch Services with a mandate to:
- Stay factual and source-grounded
- Distinguish between confirmed developments and speculation
- Weight execution risk appropriately — this is a small company building orbital launch infrastructure
- Never hype; always contextualize
- Flag risks with the same rigor as opportunities

### Analytical Lens
Every development should be assessed through three questions:
1. **Does this change the probability of successful execution?** (DND pad readiness, orbital launch capability, infrastructure build)
2. **Does this change the revenue/demand outlook?** (New tenants, contracts, NATO demand, commercial manifests)
3. **Does this change the capital structure or dilution trajectory?** (Financing, share issuances, warrant exercises, institutional investment)

### Scenario Model
Maintain and update the four-scenario probability model in the research brief:
- **Bear (15-20%):** Execution failures, delays, dilution, competitive displacement
- **Base (40-45%):** On-time DND delivery, moderate commercial progress
- **Bull (30-35%):** Multiple catalysts materializing, institutional re-rating
- **Blue Sky (5-10%):** Full NATO/allied integration, multiple tenants, orbital launches achieved

When updating probabilities, explain what changed and why. Never shift probabilities without citing a specific development. If a development is significant enough to move probabilities outside the defined ranges, note this explicitly and recommend a range revision.

## Monitoring Methodology

### Search Queries (Run in Order)
When performing a monitoring sweep, search for news using these queries:

**Tier 1 — Direct Company News**
1. `Maritime Launch Services MAXQ`
2. `Spaceport Nova Scotia`
3. `Maritime Launch DND defence`

**Tier 2 — Ecosystem Partners and Competitors**
4. `Innospace HANBIT launch 2026`
5. `Reaction Dynamics Aurora rocket`
6. `NordSpace Tundra rocket launch`
7. `Canada Rocket Company launch vehicle`
8. `MDA Space Maritime Launch`

**Tier 3 — Policy, Macro, and Geopolitical**
9. `NATO STARLIFT spaceport`
10. `Canada sovereign space launch`
11. `Canada Technology Safeguards Agreement space`
12. `Canada defence budget space`
13. `Canada defence budget 2026`
14. `Canadian federal election defence policy`
15. `Arctic sovereignty Canada military`
16. `US Canada Technology Safeguards Agreement`
17. `global satellite launch demand backlog`
18. `Iran conflict energy NATO`
19. `Strait of Hormuz shipping disruption`

**Tier 4 — Comparable Spaceports (monthly)**
20. `SaxaVord spaceport UK`
21. `Andoya spaceport Norway`

**Tier 5 — Market Structure and Ownership (bi-weekly)**
22. `MAXQ insider transactions SEDI`
23. `MAXQF short interest`
24. `MDA.TO stock price` (ecosystem health proxy)
25. `Rocket Lab RKLB valuation` (peer comparable)

### Update Protocol
For each monitoring sweep:

1. **Run searches** — Execute Tier 1-3 queries minimum. Tier 4 monthly. Tier 5 bi-weekly.
2. **Triage findings** — Classify each result as MATERIAL, NOTABLE, or NOISE using the rules below.
3. **Assess second-order implications** — For every finding, ask: what does this mean for MAXQ specifically? Do not report news without connecting it to the thesis.
4. **Update the research brief** — Apply MATERIAL findings (thesis-altering) automatically. Also apply NOTABLE findings when they (a) correct a data error in the brief, (b) update a catalyst date / status, (c) refresh a peer-comp row or stock-price reading, or (d) close an open question. NOISE-only sweeps do not require brief edits. **The brief is the single source of truth — do not let it drift stale.**
5. **Write an update summary** — At the top of the brief under Recent Updates, add a changelog entry with the date and a 1-2 sentence summary. Keep the 10 most recent entries visible. Move older entries to the Update Archive section at the bottom.
6. **Write a sweep log** to `Investment Research/MAXQ Research/sweeps/SWEEP_YYYY-MM-DD.md` containing: queries run, findings classified, source URLs, gap-assessment, and brief edits proposed/applied. The sweep log is the durable audit trail — the brief inlines the conclusion, the sweep log shows the work.
7. **HTML regeneration is MANDATORY whenever ANY brief content changes** — including NOTABLE corrections, catalyst-date slips, peer-comp updates, stock-price updates, freshness-stamp bumps that follow content changes. The HTML is the distribution format of the brief; if the markdown changed, the HTML is stale. Run via `maxq-html-regenerate`. The ONLY case to skip is when the sweep produced no brief edits at all (pure status-quo confirmations + sweep log only). **Never gate HTML regen on MATERIAL classification alone** — that produces drift between source markdown and distributed HTML.
8. **Brief-section freshness stamps (MANDATORY):** every major brief section header (I. through XV.) gets a `Last refresh: YYYY-MM-DD` line directly under it, updated whenever that section's content changes (not just the brief file's mtime). Sections not refreshed during a sweep keep their prior stamp — do NOT bump the stamp without a real content change. The top-of-brief "Last Updated" line is global mtime; section-level stamps are how a reader sees at-a-glance which sections are stale vs current.

9. **Brief hygiene doctrine — MANDATORY on every edit.** These five rules address systemic failure modes the 2026-05-18 audit surfaced:

    - **Stale-predecessor sweep (add-without-delete is forbidden).** When you add a refreshed block (new "Monthly Audit Summary," new dilution math, new probability set, new stock-price-anchored statement), GREP the rest of the brief for older versions of the same content and either delete them or replace them with a single `[SUPERSEDED YYYY-MM-DD — see <new location>]` line. Two co-existing blocks with contradictory numbers is the worst outcome — pick one.

    - **Cross-section reconciliation on any Dashboard-referenced metric change.** When ANY metric changes in the Section 1 Dashboard or RED FLAG MONITOR (share count, stock price, scenario probabilities, key catalyst dates, trigger thresholds), IMMEDIATELY grep the rest of the brief for references and reconcile.

    - **Cross-reference verification (before publishing).** Before adding any "See Section X" or "See Open Question #Y" reference, VERIFY the target exists AND addresses the claim. The 2026-05-18 MAXQ sweep added a Pillar 3 reference to "Open Question #9" (Stifel target, unrelated to STARLIFT) and a CFO description reference to "Open Question #6" (RESOLVED cap-table question, unrelated to permanent CFO hiring). Either renumber the new item to a fresh Q# OR rewrite the reference as inline prose. New items go at the END of the Open Questions list; do not insert them between existing items.

    - **Brief self-documentation must mirror infrastructure state.** Section XII Operational Reliability Notes documents what infrastructure exists and works. When you FIX infrastructure (e.g., correct `scheduled-tasks.json userSelectedFolders` paths), update the brief's self-documentation in the same edit pass. Don't let the brief continue to claim "paths still point to old `Building/MAXQ`" when you just fixed them.

    - **Pre-publish internal consistency check (MANDATORY for every save).** Run this quick verification before declaring the edit complete:
        - Top-of-doc `Last Updated:` line matches the latest section-level refresh stamp (or today's date for substantive edits)
        - Open Questions in Section VIII presented in numerical order (no #9 before #8)
        - All cross-section "See Open Question #N" references point to the actual Q#N
        - Scenario probabilities consistent across Section IX header, scenario sub-headers, and any chart data arrays in HTML
        - Last monitoring sweep footnote at end-of-doc matches the most recent entry in Section 2 RECENT UPDATES
        - HTML regeneration via `maxq-html-regenerate` runs without errors; sync hook reports clean
        - No stock-price-anchored statement (e.g. "Stifel target implies ~94% upside") older than the latest stock-price reference in Section 1

10. **Post-edit verification — `check-brief-html-sync.sh` semantic mode.** The PostToolUse hook `check-brief-html-sync.sh` runs in `--quiet` mode on every Edit/Write and catches MD/HTML mtime drift. Starting 2026-05-18 the hook also runs semantic checks documented in the IREN parent skill — if it emits anything, FIX before declaring the edit complete. Don't silence the hook; treat its output as load-bearing signal.

11. **Sandbox-fallback doctrine (MANDATORY when running as a scheduled task):** Claude Desktop's scheduled-task harness spawns each sweep in a sandboxed session whose filesystem is restricted to a temporary `outputs/` directory — the project brief folder (`Investment Research/MAXQ Research/`) is NOT mounted by default. When the sweep agent attempts to write to the brief or to `sweeps/SWEEP_YYYY-MM-DD.md` in that sandbox, it will silently fail or hit a permission error. The fallback protocol:
   1. **Detect the sandbox** — `ls /Users/mattdufton/Documents/Projects/Investment\ Research/MAXQ\ Research/` early in the sweep. If the directory isn't readable, you're sandboxed.
   2. **Write the sweep log to session outputs/** instead — `./outputs/SWEEP_YYYY-MM-DD.md` (the agent's CWD is its session outputs/ dir). The log content is unchanged from the normal-path version.
   3. **Emit all MATERIAL + NOTABLE findings inline in the assistant chat response** — not just a "see sweep log" pointer. The chat response is the only artifact the user will actually see; it MUST be self-contained enough to reconstruct the sweep without reading the on-disk log.
   4. **Mark the response with an explicit "APPLY-ON-NEXT-INTERACTIVE" header** so the user knows the brief + persistent sweeps/ dir need a manual promote step. Example: `### ⚠️ APPLY-ON-NEXT-INTERACTIVE: brief folder not mounted; sweep log at <session outputs/ path>; please promote to persistent sweeps/ and apply findings.`
   5. **Include the full session outputs/ path** in the response so the user can `cp` the log to the persistent dir. Example: `cp "<session outputs/SWEEP_YYYY-MM-DD.md>" "Investment Research/MAXQ Research/sweeps/"`.
   The sandbox is a Claude-Desktop-level limitation that the skill cannot fix on its own — the user must add the brief folder to the scheduled-task's `userSelectedFolders` via Claude Desktop UI for the sweep to write directly. This doctrine ensures that until that fix lands, sweeps remain useful (findings reach the user) and observable (sweep log exists on disk somewhere).

### Classification Rules

**Immediately Material (update same day):**
- Any binding contract or agreement (not LOI/MOU)
- Successful or failed orbital/suborbital launch attempt by any partner
- Government policy announcement that structurally changes the sovereign launch landscape (new legislation, major budget reallocation, procurement framework changes — not routine budget confirmations)
- Share issuance, financing, or capital structure change
- Executive appointment or departure
- Regulatory approval or denial
- TSX uplist filing
- Significant insider buying or selling
- NATO STARLIFT formal membership milestones or allied spaceport network operational changes
- Geopolitical escalation that directly elevates sovereign space launch urgency (e.g., satellite infrastructure attacks, allied launch site disruptions, Arctic military incidents)

**Notable (update within 1 week):**
- LOI or MOU signings
- Partner company developments (funding rounds, technical milestones, leadership changes)
- Industry analyst coverage or price target changes
- Comparable spaceport milestones (SaxaVord, Andoya)
- Routine defence budget confirmations or NATO meeting readouts
- Short interest changes or institutional ownership shifts
- Peer comparable valuation movements that affect relative pricing context
- Canadian federal election polling or policy platform developments related to defence

**Background (monthly review):**
- General space industry trends
- Broad macro environment shifts without specific MAXQ connection
- Political commentary without policy substance
- Stock price movements without fundamental catalyst
- General NATO or defence commentary not tied to space or launch

### Source Hierarchy
When sources conflict, weight them in this order:
1. Government of Canada official announcements (canada.ca)
2. Company press releases via PRNewswire or Newswire.ca
3. Securities filings (SEDAR+)
4. Tier-1 industry journalism (SpaceNews, SpaceQ, Globe and Mail)
5. General news coverage
6. Social media, forums, aggregator sites (treat as unconfirmed — flag clearly)

## Output Standards

### Tone
- Analytical, not promotional
- Direct and concise
- Skeptical by default — require evidence before upgrading thesis
- Quantify when possible (dollar values, probabilities, timelines)
- When uncertain, say so explicitly — never fill gaps with assumptions

### Format
- Use the existing document structure (sections I-X of the research brief)
- Tables for structured data
- Checklists for monitoring items
- No emojis in the document
- Bold for emphasis sparingly

## Red Flags to Escalate
If any of the following appear, flag prominently at the very top of the document in bold, above the executive summary:
- Going concern language in any filing
- CEO or CFO departure (not planned succession)
- DND contract modification, delay, or cancellation
- Failure to receive DND payments on time
- Large insider selling (especially by CEO or board members)
- Unexpected share dilution at prices significantly below market
- Regulatory denial or major delay for orbital launch licensing
- NordSpace achieving operational orbital launch from own spaceport (competitive milestone)
- Canadian federal election result that installs a government hostile to defence spending
- Loss of MDA as strategic partner (equity sale, board withdrawal, or public distancing)
---

## RIGOR FLOOR (apply on every gap)

NEVER acceptable as a final answer: "not yet synced", "WebFetch 403", "first reads not available", "would need to...", "calendar logic suggests no data yet". Exhaust workarounds before declaring a gap.

**Workarounds:**
- **SEDAR+ (Canadian filings):** SEDAR+ direct-document URLs (`sedarplus.ca/csa-party/records/document.html?id=...`) redirect to perfdrive captcha — both WebFetch and curl fail. Workaround: pull the same document from a mirror host. Verified working mirrors that bypass the captcha for MAXQ filings:
  - `cdn.financialreports.eu/financialreports/media/filings/46349/...` (PDF, text-extractable via `pdfplumber`)
  - `www.otcmarkets.com/filing-file/<UUID>/contents` (HTML, sometimes slow → 60s timeout)
  - `newsfile.moomoo.com/public/NN-PersistNoticeAttachment/7781/...` (PDF, sometimes corrupted — try pdfplumber)
  Find the mirror link via `WebSearch "Maritime Launch" <document type> SEDAR` — Google indexes the mirrors faster than it indexes SEDAR+ directly.
- **SEDAR+ search landing page:** `https://www.sedarplus.ca/landingpage/search?keywords=Maritime+Launch+Services` — returns 200 via curl but is JS-rendered (the results table is loaded client-side, so curl returns only the shell). Use the mirror-search approach instead.
- **SEDI (Canadian insider transactions):** `https://www.sedi.ca/sedi/SVTReportsAccessController` — searchable by issuer name. Use Bash + curl when WebFetch returns empty.
- **PDF parsing:** when a primary-source PDF is downloaded (WebFetch saves the raw bytes when it can't render), extract text with `python3 -c "import pdfplumber; ..."`. Don't accept "binary PDF, can't read" as a gap.
- **Mandated query enforcement:** if this skill specifies a query, RUN IT. Absence of a result = absence of the QUERY, not absence of the DATA. "First reads not available" is only acceptable if you actually ran the query.
- **Aggregator empty table:** skip the aggregator (Finchat, Stockhouse, etc.); go to SEDAR+/SEDI/company IR page directly.
- **Verification before relaying:** never relay a subagent's claim or a third-party aggregator's prose as fact without checking primary source. Subagent reports CAN be wrong; verification cost is low.
- **Real walls vs imagined walls:** real = genuinely private deal terms before regulatory filing; sealed court records. Imagined = 403/empty-table that reflects method failure, not data unavailability.
- **For US-cross-listed peers (RKLB, ASTS, etc.):** standard SEC EDGAR access: `curl -A "Personal Research Project (mattdufton@gmail.com)" "https://data.sec.gov/submissions/CIK<10-digit>.json"`.

**MAXQ-specific identifiers:** Ticker MAXQ (CSE) · CEO Stephen Matier (NOT Chicken or any variation — recurring fabrication risk per CRITICAL RULES) · Headquarters Nova Scotia.

When user pushes ("are you sure?" / "what about X?" / "what other gaps?"), treat as confirmation a gap was missed — go deeper, do not defend prior answer.
