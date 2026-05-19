# /vc-radar — VC & Investor Signal Tracker

Track what top VCs and angel investors are writing and funding. Surface emerging startup opportunities before they become consensus. Synthesize signals across multiple lenses and maintain a persistent log.

---

## How to invoke

- **Quick scan** — `vc-radar` or `vc-radar quick` — 3-5 investors, last 30 days, ~low token cost
- **Full sweep** — `vc-radar full` — all investors, last 60 days, comprehensive
- **Focused** — `vc-radar [investor name]` — deep dive on one person
- **Category** — `vc-radar [topic]` — e.g. "vc-radar martech" or "vc-radar data activation"
- **Add signal** — `vc-radar add [paste article/tweet/link]` — log a new entry manually
- **Synthesize** — `vc-radar synthesize` — cross-lens synthesis from the tracker, no new fetches

---

## The Five Lenses

Always tag every signal entry with its lens:

| Lens | Label | Who |
|------|-------|-----|
| Capital Allocation | `L1` | Elad Gil, Paul Graham, Benedict Evans, Patrick Collison, Packy McCormick, Marc Andreessen, Howard Marks, Nat Friedman (now L3), Tren Griffin |
| Technology Visionaries | `L2` | Ray Kurzweil, Jensen Huang, Demis Hassabis, Yann LeCun |
| Builder-Practitioners | `L3` | Andrej Karpathy, Aaron Levie (Box), Tobi Lütke (Shopify), Sam Altman, Sridhar Ramaswamy (Snowflake), Ali Ghodsi (Databricks), Nat Friedman (Entire) |
| Domain Experts — Martech/Data | `L4` | Scott Brinker, David Raab, Tomasz Tunguz, Chris Riccomini (Materialized View Capital) |
| Research-to-Reality | `L5` | Andrew Ng, Fei-Fei Li, Ion Stoica |

---

## Output format

Every run produces two sections:

### 1. Signal Entries (one per finding)
```
[DATE] [LENS] [INVESTOR] — [TITLE/TOPIC]
Signal: one sentence summary of the claim or bet
Implication: what this means for the martech/data/AI space
Strength: EARLY / FORMING / CONSENSUS / CONSENSUS-SHIFTING
```

### 2. Synthesis Report
```
WHERE THEY AGREE THIS SCAN
[2-3 bullet points of convergence across lenses]

NEW SIGNAL THIS SCAN
[What's materially different from the last scan]

SIGNAL STRENGTH OVERALL
[Moving from EARLY → FORMING → CONSENSUS? Holding? Reversing?]

STRATEGIC IMPLICATIONS
- TapClicks: [specific product or strategic action]
- SaaSMatchup: [positioning or content angle]
- Angel investing: [category or company type to watch]
```

---

## Persistent tracker log

Append all new signal entries to: `~/Documents/Vercel/startup-studio/vc-radar-log.md`

Format of each log entry:
```markdown
## [DATE] — [Scan type: quick/full/focused]

### Signals
[Signal entries here]

### Synthesis
[Synthesis report here]
```

If the file doesn't exist, create it with a header:
```markdown
# VC Radar Log
Persistent tracker of investor signals across 5 lenses.
Framework built from research session: March 2026.
```

---

## What to look for

**Thesis signals** — what investors are writing about, arguing for, warning against
- Blog posts, essays, interview transcripts, keynotes, tweets with investment implications
- Focus on: forward-looking claims, timing signals, specific gaps they'd fund, warnings about crowded spaces

**Funding signals** — what's actually getting capital
- YC batch announcements, Series A/B press, notable seed rounds
- Focus on: which categories are getting funded, which are being avoided, valuation signals

**Thesis divergence** — when smart people disagree
- Agreement = likely true. Divergence = likely where the opportunity is.
- Flag when two lenses point in opposite directions on the same question.

---

## Priority topics for this studio

Always flag if any signal touches:
- Marketing agents / agentic marketing operations
- Context-as-a-Service / semantic layer for enterprise data
- Marketing measurement (MMM, incrementality, attribution in a cookie-less world)
- First-party data activation for mid-market
- AgentOps / governance for marketing agent fleets
- Marketing decision memory / institutional knowledge infrastructure
- Agent-legible brand infrastructure
- The death/evolution of SaaS point solutions

---

## Seed context (do not re-fetch — already in tracker)

Key findings from the March 2026 research session:

**The convergent signal:** Karpathy, Brinker, Ghodsi, Stoica, and Sequoia all independently identified the same gap — the domain-specific context layer between enterprise data and AI agents is unbuilt. In marketing specifically: context-as-a-service, marketing decision memory, and AgentOps for agency fleets are all open categories.

**Timing:** Jensen's GTC 2026 (March 16) called the "inference inflection" — compute is now cheap enough for agents at scale. Sequoia's "This is AGI" essay (March 2026) quantified the METR curve — agent capability doubling every ~7 months, with expert-day tasks by 2027-2028.

**Bubble warning:** The infrastructure bubble (GPU clusters, foundation models) is real. The application layer (domain-specific intelligence with proprietary data) is not in the same bubble. The VC survival filter: revenue in <6 months, moat beyond the model API, no dependency on a second raise.

**TapClicks position:** 100+ ad platform connectors, normalized cross-platform marketing data at scale, agency customer base with contracts. The three-layer build: Intelligence Layer → AgentOps → Decision Memory.

**Investors already logged:**
- Benedict Evans (Feb 2026): OpenAI has no structural moat — application layer is more open than it looks
- Benedict Evans (Nov 2025): AI = biggest platform shift since iPhone, but only that. "What step can we remove" replaces "what feature to add"
- Elad Gil (Jul 2025): Vertical enterprise + proprietary data = the open market. Foundation models, coding tools, legal AI = settled
- Packy McCormick (Jan 2026): "Run up the stack" as AI commoditizes skills. Human judgment + AI = the compounding combination
- Tomasz Tunguz (Apr 2026): Anthropic commoditizing complements via MCP. Domain-specific focus is the response
- Tomasz Tunguz (Apr 2026): AI Problem Matrix — open loop (human judgment) vs closed loop (automatable). AgentOps and Decision Memory are open loop
- Tomasz Tunguz (Apr 2025, still being cited): Semantic layer = most valuable enterprise data asset by 2026
- Sequoia (Mar 2026): "This is AGI" — METR curve, talkers vs doers, $1T opportunity
- Nat Friedman (Mar 2026): Reclassified to L3. Launched Entire — $60M seed, durable context for agent collaboration
- Chris Riccomini (Apr 2026): Deep infrastructure practitioner. Portfolio: Confluent ecosystem, Databricks-adjacent (Tabular, Transform both acquired), Hypermode (agent infra), Bauplan (immutable pipeline). Signal lens: data infrastructure primitives that get absorbed into platforms
