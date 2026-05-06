# LEVIATHAN AI: Advanced Order Flow & Intelligence Trading System

> **Organization:** Black Wealth Capital
> **Project:** LEVIATHAN AI — Standalone Trading Software & Intelligence Core
> **Status:** Strategic Blueprint / Full System Architecture
> **Last Updated:** April 2026

---

## Table of Contents
1. [Vision & Core Philosophy](#vision--core-philosophy)
2. [The 12+ Domain Architecture](#the-12-domain-architecture)
3. [Global Tech Stack](#global-tech-stack)
4. [Operating Modes](#operating-modes)
5. [End-to-End Workflow](#end-to-end-workflow)
6. [Integration with ØMEGA AI](#integration-with-ømega-ai)
7. [AI-Systematic Strategy Pipeline](#ai-systematic-strategy-pipeline)
8. [TLDR: Implementation Roadmap](#tldr-implementation-roadmap)
9. [Deep Dive Documents](#deep-dive-documents)

---

## Vision & Core Philosophy

LEVIATHAN AI is the trading mind of Black Wealth Capital. It is designed as a standalone, institutionally structured, research-first trading organism. 

Its identity is not built around "prediction" — its identity is built around **capital permission**. It exists to absorb trading knowledge, transform that knowledge into structured strategy intelligence, read live markets across multiple truth layers, and decide whether capital deserves deployment.

### The 6 Core Principles
1. **Research comes before deployment**: No setup becomes live logic merely because it looks good. It must be structured, tested, and validated.
2. **Market state comes before chart pattern**: A pattern's value depends on session, prior range, volatility, and liquidity context.
3. **Order book truth outranks chart cosmetics**: If level-two flow and liquidity behavior contradict the chart, LEVIATHAN must downgrade or reject the idea.
4. **Risk is sovereign**: Risk governance is its own authority. Nothing else may override it.
5. **Execution is part of the edge**: Trade management (entry, slippage, scaling, exits) is part of the strategy, not a separate convenience.
6. **Knowledge must be ingested, but never worshipped**: Documents and books are inputs. They must be parsed, validated, and tested through research before influencing real capital.

---

## The 12+ Domain Architecture

LEVIATHAN AI is not a simple signal bot. It is an organism built from tightly connected domains that handle everything from document parsing to direct broker execution.

### 1. The Knowledge Domain
Ingests documents (PDFs, text, manuals) and converts them into structured strategy intelligence. It preserves source identity, chunks content by concept, and extracts logic into structured components. **Critical Rule**: Document knowledge must never go directly to live execution without passing through the Research Domain.

### 2. The Research Domain
The strategy laboratory. Generates code (Pine Script, Python, MT5 EA), tests across sessions and volatility, and performs walk-forward analysis and Monte Carlo resilience testing. Every strategy becomes a structured **Strategy Genome** containing 40+ fields.

### 3. The Signal Domain
The chart and structure interpreter. Detects Market Structure Breaks (MSB/BOS), trend state, moving averages, volatility compression/expansion, and reversal/continuation patterns.

### 4. The Session & Range Domains
- **Session Domain**: Treats time-of-day as a first-class edge (Asian, London Open, NY Overlap). Knows when breakouts are trustworthy and when dead-time quality collapses.
- **Previous Day & Range Domain**: Tracks and interprets PDH, PDL, midpoint, overnight highs/lows, and opening ranges.

### 5. The State & Liquidity Domains
- **State Domain**: Treats the market as a moving state machine (compression, expansion, breakout, exhaustion, reversal, hazard).
- **Liquidity Domain**: Quantifies smart money concepts (equal highs/lows, pools, FVGs, sweep/reclaim, failed auctions).

### 6. The Truth Domain
Validates or rejects chart-side ideas using live market behavior across 4 sub-layers:
1. **Level 2 / Order Book**: Bid/ask imbalance, spoofing, absorption, exhaustion, vacuums.
2. **Options Context**: Call/put pressure, unusual derivatives activity.
3. **Economic Event**: Classifies time windows (safe, reduced-risk, no-trade).
4. **Sentiment Context**: Evaluates narrative shock (bounded modifier).

### 7. The Visual Overlay Domain
Renders advanced market intelligence over TradingView-style charts. Shows liquidity heatmap bands, market profiles, volume concentration, and order-book density zones in a clean, low-opacity interface.

### 8. The TradingView Bot Layer
The chart-to-intelligence bridge. Receives TradingView webhooks, maps them to LEVIATHAN strategy families, enriches with session/state context, passes to Truth Domain for verification, and renders response back to user workflow.

### 9. The Execution & Broker Plug-In Layer
Supports two major execution spines:
1. **Direct Broker**: Order routing, bracket logic, reconciliation, account-state awareness.
2. **MetaTrader 5 (EA) Domain**: Full execution sub-framework. Supports staged entries, trailing logic, session-aware execution, and **prop firm mode** (enforcing daily drawdown, loss-streak throttles, and consistency logic locally).

### 10. The Decision & Risk Governance Domains
- **Decision Domain**: Consumes all domains to output permission (reject, wait, approve, signal-only) along with direction, confidence, entry style, scaling permission, and prop firm safety status.
- **Risk Governance (Sovereign)**: Governs max risk, daily/trailing drawdown, portfolio heat, event restrictions. Can veto trades, reduce size, force signal-only mode, or halt trading entirely. Nothing overrides this domain.

### 11. The Position Management & Memory Domains
- **Position Management**: Governs probe entries, partial profit taking, break-even transitions, runner preservation, and trailing escalation.
- **Memory Domain**: Records every candidate setup, session label, state label, decision explanation, entry, exit, MAE, MFE, and outcome. Drives self-improvement via drift detection and strategy promotion/retirement.

### 12. Named Internal Sub-Agents
LEVIATHAN AI can retain the same architectural information while adopting clearer internal naming. The first two named sub-agents in the current naming pass are **ORCA AI** and **MEGALODON AI**.

| Sub-Agent | Primary Role | Responsibility Within LEVIATHAN AI |
|---|---|---|
| **ORCA AI** | Market sensing and validation core | Owns signal interpretation, market-state enrichment, liquidity reading, and truth-layer synthesis before capital is approved. |
| **MEGALODON AI** | Execution and apex deployment core | Owns execution orchestration, position management, and high-conviction deployment enforcement after Decision and Risk governance have aligned. |

These names are intentionally additive and do not change the underlying architecture. They provide the first internal naming anchors while the remaining sub-agent naming set is still being finalized.

---

## Global Tech Stack

LEVIATHAN AI relies on a modern, high-performance tech stack to execute its architecture:

| Category | Technology |
|----------|------------|
| **Orchestration** | LangGraph (cyclic reasoning), PydanticAI (type-safe schemas) |
| **Intelligence** | DeepSeek-V3 (Decision Engine), Gemini 2.5 Flash (Vision) |
| **Backend** | Python 3.11+, FastAPI (API Gateway), Redis (State) |
| **Database** | PostgreSQL + TimescaleDB (Journals), Pinecone (Vector Storage) |
| **Market Data** | Bookmap/Rithmic (Level 2), Unusual Whales (Options), Polygon.io |
| **Execution** | IBKR/CCXT (Direct Broker), MT5/MQL5 (Expert Advisor) |
| **Frontend** | React/Next.js, Lightweight Charts (TradingView) |

---

## Operating Modes

LEVIATHAN AI adapts to different environments and risk tolerances:
- **Research Mode**: Testing and generation only. No live execution.
- **Advisory Mode**: Signals and plans only.
- **Semi-Automatic Mode**: Execution allowed only after full truth and risk checks (manual trigger).
- **Full Automatic Mode**: Execution allowed for fully validated strategies with all layers active.
- **Prop Firm Mode**: Stricter drawdown, tighter risk, consistency-preserving logic.
- **Recovery Mode**: Reduced execution after damage or instability.
- **Signal-Only Restriction Mode**: Execution blocked due to event risk, but signals continue.

---

## End-to-End Workflow

**Live Market Flow:**
1. TV Bot Layer generates candidate setup.
2. Session Domain classifies time context.
3. Previous Day/Range Domain classifies range context.
4. State Domain classifies market condition.
5. Liquidity Domain adds structure intelligence.
6. Truth Domain validates via order book, flow, and options.
7. Event Domain adds restrictions.
8. Sentiment Domain adds modifiers.
9. Decision Domain determines if capital is justified.
10. Risk Governance Domain vetoes, reduces, or permits.
11. Execution Domain routes via Direct Broker or MT5.
12. Position Management Domain manages the live trade.
13. Memory Domain records full lifecycle.
14. Research Domain re-mines data for evolution.

---

## Integration with ØMEGA AI

While LEVIATHAN AI is a standalone organism, it connects to the broader ØMEGA AI orchestrator as a specialized peer through the `QUANTUM` agent. Internally, LEVIATHAN’s first two explicitly named trading sub-agents are **ORCA AI** and **MEGALODON AI**. It communicates via a **dedicated status protocol**:
- **Status Heartbeat**: Broadcasts current bias, market regime, and confidence.
- **Inquiry/Response**: ØMEGA sends a signal; LEVIATHAN returns a validated Confidence Score.
- **Kill Switch Sync**: A global halt in either system triggers a halt in the other.

---

## AI-Systematic Strategy Pipeline

LEVIATHAN AI uses Claude Code's proven architectural patterns as the execution engine for its original 4-layer framework. The system does not just signal — it researches, backtests, filters, and implements strategies automatically.

### How It Works

| Layer | What the AI Does | Claude Code Pattern |
|-------|------------------|--------------------|
| **1. Research** | Gathers market data across all domains in parallel using isolated sub-agents. Each domain (Truth, Signal, Session) runs in `bubble` permission mode — it can read but never execute. | Sub-Agent Pattern, Fork Agents, Context Compression |
| **2. Backtest** | Generates strategy genomes via ULTRAPLAN (30-min cloud Opus session), then runs 50 parallel Monte Carlo simulations using fork agents that share a single prompt cache (90% cost reduction). | ULTRAPLAN, Fork Agents, Self-Describing Tools |
| **3. Iterate** | KAIROS mode logs every trade outcome. Background extraction agents mine lessons nightly. Staleness system flags strategies older than 14 days for re-validation. `/dream` consolidation prunes memory. | KAIROS, Staleness, Background Extraction, /dream |
| **4. Implement** | Async generator loop powers the 14-step Live Market Flow. Stop hooks verify every trade before broker submission. Snapshot security freezes risk params at session start. | Async Generator, Stop Hooks, Snapshot Security |

### Strategy Filtering (8 Stages)

| Stage | Layer | Criteria | Survival |
|-------|-------|----------|----------|
| Initial Generation | 2 | ULTRAPLAN generates genome | 100% |
| Monte Carlo Backtest | 2 | Sharpe > 1.5, Max DD < 15%, Win Rate > 55% | ~20% |
| Walk-Forward Validation | 2 | Out-of-sample within 80% of in-sample | ~10% |
| Regime Testing | 2 | Profitable in 3+ of 5 volatility regimes | ~5% |
| Staleness Check | 3 | Backtested within last 14 days | Removes stale |
| Memory Cross-Reference | 3 | No contradicting lessons in Trader Profile | Removes conflicting |
| Live Paper Trade | 3-4 | 2-week paper trade in Signal-Only mode | ~2-3% |
| Full Deployment | 4 | Approved for live execution | Final survivors |

### Automated Deployment

Surviving strategies are auto-generated as MT5 EAs or Pine Scripts, deployed in Semi-Auto mode, promoted to Full Auto after 10 matching trades, and auto-demoted if performance deviates by >2σ from backtest expectations.

---

## TLDR: Implementation Roadmap

For CodeSpring or any development orchestrator, follow these phases:

1. **Phase 1: Knowledge & Research**: Implement the Knowledge Domain (document ingestion via LlamaParse) and Research Domain (strategy genome) to ensure no strategy goes live without validation.
2. **Phase 2: Signal & State**: Build the TV Bot Layer and background workers to track sessions, ranges, and market states.
3. **Phase 3: The Truth Domain**: Connect to Level 2 / Bookmap-style data feeds and Unusual Whales to validate chart signals.
4. **Phase 4: Decision & Risk**: Hard-code the sovereign Risk Engine and implement LangGraph + DeepSeek-V3 for the Decision Engine.
5. **Phase 5: Execution Spines**: Build the dual execution paths — Direct Broker API (CCXT/IBKR) and the MetaTrader 5 Expert Advisor (with built-in Prop Firm mode).
6. **Phase 6: Visual Overlay**: Implement the low-opacity visual overlay for TradingView-style charts using Lightweight Charts.

---

## Deep Dive Documents

This repository contains detailed research, architecture, and specification documents. Use the links below to navigate directly to specific areas of the LEVIATHAN AI platform.

### 🌟 The Master Blueprint
* [**CODESPRING-MASTER-INSTRUCTIONS.md**](./CODESPRING-MASTER-INSTRUCTIONS.md) — The definitive 12-domain implementation blueprint with tech stack, instructions, and transferable architecture patterns.
* [**claude-code-transferable-architecture.md**](./docs/claude-code-transferable-architecture.md) — **CORE**: Claude Code's 14 battle-tested patterns mapped into the 4-layer Research → Backtest → Iterate → Implement framework, with the AI-systematic strategy pipeline, 8-stage filtering, and automated deployment logic.
* [**oracle-full-master-writeup.md**](./docs/oracle-full-master-writeup.md) — The original 1,000+ line system design narrative containing the pure logic and philosophy of the system.
* [**CODESPRING-INTEGRATION-MANIFEST.md**](./CODESPRING-INTEGRATION-MANIFEST.md) — Phase 1 integration targets.

### 🏛️ Legacy Architecture & Prompts
* [oracle-trading-system.md](./docs/oracle-trading-system.md) — Legacy 4-layer architectural overview.
* [protocol-spec.md](./docs/protocol-spec.md) — Communication with ØMEGA AI.
* [layer1-data-pipeline.md](./architectures/layer1-data-pipeline.md) — Tick data & options flow logic.
* [layer2-vision-analysis.md](./architectures/layer2-vision-analysis.md) — Chart parsing & visual intelligence.
* [decision-engine-prompt.md](./prompts/decision-engine-prompt.md) — Layer 4 synthesis prompt.
* [alignment-check.md](./prompts/alignment-check.md) — Final "GO/NO-GO" verification prompt.

### 🛡️ Security & Risk
* [capital-preservation-rules.md](./security/capital-preservation-rules.md) — Hard-coded risk constraints.
* [api-key-isolation.md](./security/api-key-isolation.md) — Sandbox & credential security.

---

**LEVIATHAN AI — Built for Black Wealth Capital.**

---
## Additive Pre-CodeSpring Implementation Appendices
These documents were added as **non-destructive handoff extensions** to make the LEVIATHAN repository more executable for implementation without removing any original architecture material.

| Document | Purpose |
|---|---|
| [additive-implementation-priorities.md](./docs/additive-implementation-priorities.md) | Defines the first real working layer of LEVIATHAN and includes code examples for the first paper-trading path. |
| [omega-prime-integration-alignment.md](./docs/omega-prime-integration-alignment.md) | Aligns LEVIATHAN’s platform integration language with ØMEGA AI and PRIME as the canonical top-level controller. |
| [oracle-schema-contracts-and-example-payloads.md](./docs/oracle-schema-contracts-and-example-payloads.md) | Establishes the core layer-1 trading schemas and example JSON payloads for setup, truth, decision, risk, execution, and journaling. |
| [market-state-transition-matrix.md](./docs/market-state-transition-matrix.md) | Makes the state/regime model explicit with transition rules, policy semantics, and code examples. |
| [risk-veto-policy-matrix.md](./docs/risk-veto-policy-matrix.md) | Defines when the sovereign risk engine can reduce, block, or halt trades and includes example veto logic. |
| [paper-trade-replay-example.md](./docs/paper-trade-replay-example.md) | Shows one full paper-trade replay from signal ingress through journal output. |
| [implementation-module-map.md](./docs/implementation-module-map.md) | Maps the documentation into a concrete proposed codebase structure and build order for CodeSpring. |

### TLDR: What These Additions Do
These appendices make LEVIATHAN AI more **implementation-ready** rather than merely more verbose. They give CodeSpring a stricter schema layer, clearer state logic, explicit risk-veto behavior, a replayable first execution path, and a cleaner module map for building the system.


---

## Additional Feature Extension: LEVIATHAN Market Intelligence Terminal

LEVIATHAN AI can absorb the full **Bloomberg-style terminal layer** represented by the BB-Terminal project and treat it as an operator-facing extension inside the broader LEVIATHAN architecture. In practical terms, this means LEVIATHAN would not only govern truth, risk, execution, and memory, but would also expose a fast visual **market-intelligence workstation** that allows a trader, analyst, or supervisor to interrogate markets through function codes rather than navigating fragmented dashboards.

This extension is valuable because it transforms several LEVIATHAN domains into an immediately usable interface. The **Signal Domain**, **State Domain**, **Truth Domain**, **Visual Overlay Domain**, and parts of the **Memory / Decision workflow** can be surfaced through a terminal-style command layer that is lightweight, auditable, and fast to operate.

### What This Extension Adds to LEVIATHAN

| Extension Capability | What It Adds Inside LEVIATHAN | Why It Matters |
|---|---|---|
| **Command Center terminal home screen** | A single screen for indices, yield curve, FX majors, crypto, movers, and headline context | Gives LEVIATHAN an operator briefing layer rather than only backend orchestration |
| **INTEL scorecard** | A structured verdict engine that converts raw data into auditable bullish / neutral / bearish rule outcomes | Matches LEVIATHAN’s need for interpretable pre-trade intelligence rather than black-box signals |
| **Function-code workflow** | Fast command syntax for intelligence retrieval such as `INTEL`, `KEY`, `QR`, `OMON`, and `CURV` | Creates a professional terminal workflow for analysts and traders |
| **Transparent rules engine** | Signal logic based on explicit thresholds instead of opaque predictions | Aligns with LEVIATHAN’s capital-permission philosophy and sovereign review model |
| **OpenBB-backed data access** | Broad market and company data coverage through a unified data interface | Provides a practical data spine for early-stage market intelligence features |
| **React + TypeScript workstation UI** | A deployable front-end layer that can later be re-skinned into LEVIATHAN branding | Reduces time-to-interface for live productization |
| **Terminal command bar + workspace tabs** | Human-usable multi-panel market workflow | Makes LEVIATHAN usable as a product, not just a concept stack |

### Terminal Function Surface That Can Be Imported into LEVIATHAN

The BB-Terminal project already defines a strong first-layer functional surface that maps well into LEVIATHAN’s operator console. Those functions can be adopted as-is initially, then extended with LEVIATHAN-specific truth, execution, and risk overlays.

| Function Code | Current Capability | LEVIATHAN Mapping |
|---|---|---|
| `CC` | Command Center dashboard | Global pre-session market briefing layer |
| `HELP` | Function directory | Operator assist and command discovery |
| `<TICKER>` / `INTEL` | Synthesized equity intelligence scorecard | Signal + truth pre-decision summary |
| `DES` | Company description / profile | Research / issuer context |
| `GP` | Multi-period candlestick chart | Chart-side structure and visual review |
| `QR` | Live quote panel | Quote monitoring and trigger awareness |
| `HP` | Historical prices | Contextual price analysis and replay |
| `FA` | Five-year financial statements | Research and valuation context |
| `KEY` | Ratios and key metrics | Valuation / quality / screening layer |
| `DVD` | Dividend history | Income and capital-return context |
| `EE` | Analyst targets and recommendation data | External expectation benchmarking |
| `NI` | Company news | Narrative / event context |
| `OMON` | Options chain monitor | Derivatives context for the Truth Domain |
| `WEI` | World equity indices | Cross-market regime awareness |
| `MOV` | Gainers / losers / active names | Opportunity discovery and anomaly scanning |
| `CRYPTO` | Crypto dashboard | Multi-asset surveillance extension |
| `FXC` | Major FX pairs | Macro and cross-asset context |
| `CURV` | Treasury yield curve and spreads | Macro regime, liquidity, and recession-signal context |

### How This Fits the Existing LEVIATHAN Architecture

This extension should be treated as a **LEVIATHAN-facing market interface module**, not as a replacement for the sovereign architecture already defined in this repository. Its best fit is as a product-facing layer that sits on top of LEVIATHAN’s institutional logic.

| Existing LEVIATHAN Domain | BB-Terminal Contribution | Resulting Combined Feature |
|---|---|---|
| **Signal Domain** | INTEL, GP, HP, KEY | Faster chart + metric interpretation for live candidates |
| **Truth Domain** | OMON, NI, CURV, FXC, WEI | Better contextual confirmation before permissioning capital |
| **Research Domain** | DES, FA, KEY, HP | Faster research pull-through into the strategy workflow |
| **Visual Overlay Domain** | Terminal layout, command center, workspace tabs | A usable trader-facing interface shell |
| **Decision Domain** | Rule-based summaries from `signals.ts` | Transparent pre-decision evidence display |
| **Memory / Replay** | Historical panels and rule outputs | Easier journaling, review, and post-trade audit surfaces |

### Technical Extension Profile

The BB-Terminal stack is a strong fit for an early LEVIATHAN interface layer because it is already broken into a clean API + UI pattern.

| Layer | Imported Stack | LEVIATHAN Extension Role |
|---|---|---|
| **Market API** | OpenBB Platform on FastAPI / Uvicorn | Early-stage market-data abstraction layer |
| **UI Framework** | Vite + React + TypeScript | Terminal workstation shell |
| **Charts** | TradingView Lightweight Charts | Visual market review and operator workflow |
| **Rule Engine** | `app/src/lib/signals.ts` | First interpretable evidence engine before LEVIATHAN-specific truth models |
| **Command System** | CommandBar + WorkspaceTabs + FunctionPanel | Human interface to LEVIATHAN intelligence |

### Productization Interpretation Inside LEVIATHAN

If incorporated correctly, this should be presented as a new LEVIATHAN feature rather than a separate unrelated repo. The clean framing is that LEVIATHAN gains a **Market Intelligence Terminal** extension that gives users a professional operator environment for discretionary review, semi-automated supervision, and eventually governed live deployment.

This means the imported terminal should initially serve three roles. First, it becomes the **research and market-briefing console** for analysts. Second, it becomes the **pre-trade verification console** for ORCA AI as it interprets state, liquidity, and external context. Third, it becomes the **execution supervision console** that MEGALODON AI can use as a visible operator layer once order-routing and broker interfaces are wired in.

### Practical Implementation Positioning

The BB-Terminal codebase is especially useful because it already proves a first working surface for:

| Already Implemented in the Source Project | Immediate Value to LEVIATHAN |
|---|---|
| Local launch scripts (`setup.sh`, `start.sh`, `stop.sh`) | Fast developer onboarding for the interface layer |
| Command-driven terminal workflow | Makes the platform feel like a real institutional product early |
| Multi-function panels across equities, macro, FX, crypto, and options | Gives LEVIATHAN a broad market context shell before bespoke feeds are wired in |
| Transparent rule-based scoring | Preserves explainability and supports governed decision review |
| OpenBB provider abstraction | Accelerates early data integration without building everything from zero |

### Known Constraints to Respect During Integration

This extension should be adopted with discipline. The imported project is a strong interface and intelligence shell, but it does **not** replace the deeper institutional layers already defined in LEVIATHAN.

| Constraint | Meaning for LEVIATHAN |
|---|---|
| **Polling, not true streaming** | It is suitable for early intelligence and supervision, but not sufficient alone for high-frequency or order-book-grade live execution |
| **Provider limitations** | Some advanced economic, options, and global data features depend on additional provider credentials |
| **Rule heuristics are not final decision logic** | The existing signals are useful as evidence summaries, but LEVIATHAN’s sovereign decision and risk engines must remain authoritative |
| **UI is terminal-focused, not full governance software** | It should be treated as an extension shell that later inherits LEVIATHAN’s own permissions, journaling, and execution audit layers |

### Recommended Naming Inside LEVIATHAN

Within this repository, the imported capability should be referred to as the **LEVIATHAN Market Intelligence Terminal**. That naming keeps the feature native to LEVIATHAN while still preserving the reality that the first implementation is derived from the BB-Terminal codebase and function design.

### TLDR: Why This Belongs in LEVIATHAN

This extension gives LEVIATHAN an immediately usable trader-facing product layer. Instead of waiting until every sovereign domain is fully built before the platform becomes visible, LEVIATHAN can expose a working terminal that already supports multi-asset monitoring, interpretable scorecards, options and macro context, and command-driven research workflows. In other words, the BB-Terminal project provides the **operator console**, while LEVIATHAN continues to provide the **governed trading organism** behind it.

References

[1]: https://github.com/vaughanf1/BB-Terminal "vaughanf1/BB-Terminal"
[2]: https://github.com/OpenBB-finance/OpenBB "OpenBB Platform"
