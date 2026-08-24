# /tech-radar — AI Infra & Tooling Technology Radar

Track where to place engineering bets across AI infrastructure categories. ThoughtWorks-style Adopt/Trial/Assess/Hold radar, always read against the studio's actual builds — TapClicks DAP, the GKE fine-tuning lab, ObsGap, and weekend-scale projects — not abstract industry commentary.

---

## How to invoke

- **Quick pulse** — `tech-radar` or `tech-radar quick` — 1-2 categories, most recent movers only, low token cost
- **Full sweep** — `tech-radar full` — all tracked categories, comprehensive
- **Category deep dive** — `tech-radar [category]` — e.g. `tech-radar inference serving` or `tech-radar agent frameworks`
- **Add a category** — `tech-radar add [category name]` — expand the tracked quadrant set (log it as a new C-code)
- **Synthesize** — `tech-radar synthesize` — cross-category synthesis from the log, no new research
- **Visual** — `tech-radar visual` — regenerate the HTML radar artifact from the current log state (see Visual rendering below)

---

## Tracked categories (the four quadrants)

| Code | Category | What it covers |
|------|----------|-----------------|
| C1 | Agent Orchestration & Frameworks | LangGraph, Claude Agent SDK, CrewAI, AutoGen/Microsoft Agent Framework, OpenAI Agents SDK, etc. |
| C2 | Inference & Serving | vLLM, SGLang, TensorRT-LLM, managed inference APIs |
| C3 | Context & Data Infra | Semantic layers (Cube, dbt), vector DBs (pgvector, Pinecone, Turbopuffer), MCP as the context-exposure protocol |
| C4 | AgentOps & Evals | LangSmith, Braintrust, Langfuse, Arize Phoenix |
| C5 | Conversational & Agentic BI | Snowflake Cortex Analyst, Databricks Genie, ThoughtSpot Spotter, generic text-to-SQL agents |
| C6 | Decision Intelligence & Autonomous Decisioning | Aera Technology, Palantir AIP, marketing-specific auto-optimization/decisioning |
| C7 | Marketing Measurement AI | MMM/incrementality/attribution — Google Meridian, Meta Robyn, PyMC-Marketing, Recast, the triangulation practice |
| C8 | Embedded AI in Incumbent BI | Power BI Copilot, Tableau Pulse/Einstein, Domo AI/Sigma/Knowi/Qlik — the AI-bolted-onto-dashboards layer |

Add new categories only when a real recurring signal doesn't fit the four above (e.g. fine-tuning/training infra, multi-agent coordination standards, edge/on-device). Log new codes (C5, C6, ...) in the tracker header when added.

---

## The rings (ThoughtWorks convention, center to edge)

| Ring | Meaning |
|------|---------|
| **Adopt** | Safe default. Use it now, no caveats. |
| **Trial** | Worth piloting on real work, not yet the default. |
| **Assess** | Worth understanding; not yet worth committing to. |
| **Hold** | Proceed with caution — usually a stack-fit problem, not a quality one. Say *why* it's held (model lock-in, ops burden, no traction) rather than just "avoid." |

---

## Output format

Every run produces entries plus a synthesis, in the same shape as the persistent log (below).

### 1. Entries (one per finding)
```
[RING] [CATEGORY-CODE] Name
Rationale: one or two sentences — what it is, why this ring, and (where relevant) which studio project it actually touches
```

### 2. Synthesis
```
CROSS-CUTTING READ
[2-4 bullets: what the ring distribution says, what's new since the last scan, where categories converge]

STRATEGIC IMPLICATIONS
- TapClicks/DAP: [specific product implication]
- GKE fine-tuning lab: [specific build implication]
- ObsGap / studio builds: [specific tooling choice]
- Weekend-scale projects: [default recommendation]
```

Always tie rationale back to a real studio project when one applies — a radar entry that's pure industry commentary with no "so what for me" is incomplete.

---

## Persistent tracker log

Append all new entries to: `~/Documents/Vercel/startup-studio/tech-radar-log.md`

Format of each log entry:
```markdown
## [DATE] — [Scan type: quick/full/category deep dive/synthesize]

### Categories tracked this scan
[which C-codes were touched]

### Entries
[entries here]

### Ring counts this scan
Adopt: N · Trial: N · Assess: N · Hold: N (of TOTAL)

### Synthesis
[synthesis report here]
```

If the file doesn't exist, create it with a header:
```markdown
# Tech Radar Log
Persistent tracker of engineering-bet signals across AI infra categories.
ThoughtWorks-style rings (Adopt / Trial / Assess / Hold), read against actual studio builds.
Framework built from research session: [date].
```

Before writing a new entry, re-check any blip already logged in a prior scan — if its ring changed, say so explicitly (`SGLang: Trial → Adopt`) rather than silently re-listing it. Ring movement between scans is itself a signal worth calling out in the synthesis.

---

## Visual rendering

A companion HTML radar chart (ThoughtWorks-style quadrant/ring visualization, self-contained static file) can be generated from the log on request — via the `artifact-design` + `artifact-diagramming` skills, published as a Claude Artifact and also saved as a static file to `~/Documents/Vercel/startup-studio/dashboards/tech-radar.html`. The visual is a rendering of the log, not a separate source of truth — regenerate it after any full sweep or synthesize run that changes ring placements; don't hand-maintain it independently of the log.

---

## What to look for

**Adoption signals** — production deployment footprint, download/star trends, "default recommendation" language in comparison posts
**Performance signals** — benchmark deltas that are large enough to matter (>15-20%), not noise
**Consolidation signals** — mergers, one tool absorbing another's use case (e.g. Microsoft Agent Framework absorbing Semantic Kernel + AutoGen)
**Stack-fit signals** — model lock-in, protocol lock-in, or ops-burden reasons a tool doesn't fit *this* stack specifically (Claude-centric, LangGraph-anchored, Postgres-first, GKE-hosted)

---

## Priority framing for this studio

Every entry should implicitly or explicitly answer: does this change what TapClicks DAP should build vs. buy, what the GKE fine-tuning lab should run, how the ObsGap multi-agent rebuild should be architected, or what the default stack is for a new weekend project? A signal that doesn't touch any of these is still worth logging (market awareness has value) but should be flagged as background, not action-relevant.

---

## Seed context (do not re-fetch — already in tracker)

From the 2026-08-22 founding scan:

**The Adopt ring is deliberately boring:** LangGraph, Claude Agent SDK, vLLM, MCP, pgvector — the load-bearing defaults, not exotic bets.

**Where the studio should be watching hardest:** Context & Data Infra (C3). Cube's "one metric definition, four APIs including MCP" is close enough to what TapClicks DAP would need to build in-house that it's worth a real trial before building it from scratch. Turbopuffer's per-namespace model maps directly onto TapClicks' per-agency data isolation.

**GKE lab:** vLLM is the serving default; SGLang (RadixAttention, ~29% throughput gain on prefix-heavy traffic) is the one worth a bake-off given agent workloads' repeated-system-prompt shape.

**ObsGap rebuild:** Claude Agent SDK + LangGraph is the natural orchestrator pairing (scanner/analyzer/ranker/writer with state handoff) — both already Adopt-ring.

**Weekend-scale default:** pgvector over Pinecone — no separate vector-DB bill, reuses existing Postgres.
