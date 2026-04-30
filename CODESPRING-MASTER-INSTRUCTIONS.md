# 🔮 CODESPRING MASTER INSTRUCTIONS: LEVIATHAN AI (BLACK WEALTH CAPITAL)

> **Role**: Lead Quantitative Developer & Systems Architect
> **Objective**: Implement the LEVIATHAN AI Standalone Trading System & ØMEGA AI Intelligence Core.
> **Status**: Hyper-Detailed Implementation Blueprint (Institutional-Grade)
> **Last Updated**: April 2026

---

## 1. Prime Directive & Core Identity

LEVIATHAN AI must be designed as a standalone, institutionally structured, research-first trading organism for Black Wealth Capital. It is **not** a simple signal bot, a chart indicator pack, a broker add-on, or a generic AI assistant. 

Its core identity is built around **capital permission**, not just prediction. It exists to answer:
- What kind of environment is the market in right now?
- Which strategy family is compatible with this environment?
- Does the current setup deserve risk?
- Is order-book behavior supporting or rejecting what the chart suggests?
- Is this setup safe under prop firm rules?

LEVIATHAN AI functions simultaneously as a research laboratory, strategy compiler, chart-intelligence layer, market-state interpreter, level-two truth engine, risk governance engine, and visual overlay engine.

---

## 2. Core Philosophy

LEVIATHAN AI operates on six non-negotiable principles:
1. **Research comes before deployment**: No setup becomes live logic merely because it looks good. It must be structured, tested, and validated.
2. **Market state comes before chart pattern**: A pattern's value depends on session, prior range, volatility, and liquidity context.
3. **Order book truth outranks chart cosmetics**: If level-two flow and liquidity behavior contradict the chart, ORACLE must downgrade or reject the idea.
4. **Risk is sovereign**: Risk governance is its own authority. Nothing else may override it.
5. **Execution is part of the edge**: Trade management (entry, slippage, scaling, exits) is part of the strategy, not a separate convenience.
6. **Knowledge must be ingested, but never worshipped**: Documents and books are inputs. They must be parsed, validated, and tested through research before influencing real capital.

---

## 3. Full System Architecture: The 12+ Domains

LEVIATHAN AI is built as a tightly connected organism comprising the following specialized domains.

### 3.1 The Knowledge Domain
Ingests documents (PDFs, text, manuals) and converts them into structured strategy intelligence.
- **Ingestion**: Preserves source identity, page numbers, section boundaries, and table structures.
- **Structuring & Classification**: Breaks documents into chunks tagged as entry rules, stop-loss methods, scaling methods, etc.
- **Extraction**: Converts logic into structured components (entry conditions, invalidation, timeframe assumptions).
- **Critical Rule**: Document knowledge must **never** go directly to live execution. It must pass through the Research Domain first.

### 3.2 The Research Domain
The strategy laboratory where knowledge becomes weaponized.
- **Function**: Generates code (Pine Script, Python, MT5 EA), tests across sessions/volatility, performs walk-forward analysis and Monte Carlo resilience testing.
- **Strategy Genome**: Every strategy is a structured object containing 40+ fields (family, supported markets, session dependencies, state dependencies, scaling rules, failure modes, prop firm suitability).

### 3.3 The Signal Domain
The chart and structure interpreter. Generates candidate setups (never grants capital permission alone).
- **Interpreters**: Market structure (MSB/BOS), trend state, moving averages, volatility compression/expansion, liquidity maps, reversal/continuation patterns.

### 3.4 The Session Domain
Treats time-of-day behavior as a first-class edge.
- **Models**: Asian session, London open/continuation, NY open/overlap/midday/close, rollover zones.
- **Logic**: Knows when breakouts are trustworthy, when range behavior dominates, and when dead-time quality collapses.

### 3.5 The Previous Day & Range Domain
Continuously tracks and interprets structural boundaries.
- **Levels**: PDH, PDL, midpoint, close, overnight H/L, session H/L, opening range H/L.
- **Logic**: Determines if price is inside, above, below, sweeping, reclaiming, or rejecting these key reference levels.

### 3.6 The State Domain
Treats the market as a moving state machine.
- **States**: Compression, expansion, trend continuation, broad/narrow range, breakout (and failure), drift, exhaustion, reversal, instability, hazard.
- **Logic**: Determines transition likelihood and which strategy families are currently compatible.

### 3.7 The Liquidity Intelligence Domain
Quantifies smart money concepts into measurable features.
- **Features**: Equal highs/lows, liquidity pools, inducement zones, FVGs, imbalances, displacement, sweep/reclaim, failed auctions.

### 3.8 The Truth Domain
Validates or rejects chart-side ideas using live market behavior.
- **Level 2 / Order Book**: Bid/ask imbalance, liquidity stacking/pulling, spoofing, absorption, exhaustion, vacuums.
- **Options Context**: Call/put pressure, unusual derivatives activity, strike clustering.
- **Economic Event**: Classifies time windows (safe, reduced-risk, no-trade).
- **Sentiment Context**: Evaluates narrative shock (bounded modifier, cannot override chart/order-book truth).

### 3.9 The Visual Overlay Domain
Renders advanced market intelligence over TradingView-style charts.
- **Visuals**: Liquidity heatmap bands, market/session profiles, volume concentration, order-book density zones, sweep/reclaim zones, AI confidence highlights, dynamic S/R shading.
- **Philosophy**: Must remain readable as a low-opacity intelligence layer translating hidden structure into visible context.

### 3.10 The TradingView Bot Layer
The chart-to-intelligence bridge.
- **Function**: Receives TradingView webhooks, maps them to ORACLE strategy families, enriches with session/state context, passes to Truth Domain for verification, and renders response back to user workflow.

### 3.11 The Execution & Broker Plug-In Layer
Supports two major execution spines:
1. **Direct Broker**: Order routing, bracket logic, reconciliation, account-state awareness.
2. **MetaTrader 5 (EA) Domain**: Full execution sub-framework. Supports signal-relay, execution-only, strategy-native, and risk-governance EAs. Handles staged entries, trailing logic, session-aware execution, and **prop firm mode** (enforcing daily drawdown, loss-streak throttles, and consistency logic locally).

### 3.12 The Decision & Risk Governance Domains
- **Decision Domain**: Consumes all domains to output permission (reject, wait, approve, signal-only) along with direction, confidence, entry style, scaling permission, and prop firm safety status.
- **Risk Governance (Sovereign)**: Governs max risk, daily/trailing drawdown, portfolio heat, event restrictions. Can veto trades, reduce size, force signal-only mode, or halt trading entirely. Nothing overrides this domain.

### 3.13 The Position Management & Memory Domains
- **Position Management**: Governs probe entries, partial profit taking, break-even transitions, runner preservation, and trailing escalation.
- **Memory Domain**: Records every candidate setup, session label, state label, decision explanation, entry, exit, MAE, MFE, and outcome. Drives self-improvement via drift detection and strategy promotion/retirement.

---

## 4. End-to-End Operating Workflow

### 4.1 Knowledge Flow
1. Document uploaded → 2. Ingested by Knowledge Domain → 3. Chunked, classified, embedded → 4. Logic extracted → 5. Compiled into strategy candidates → 6. Tested by Research Domain → 7. Surviving ideas become Strategy Genomes.

### 4.2 Live Market Flow
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

## 5. Global Tech Stack

The final build must integrate these technologies to support all 12+ domains.

### 5.1 Orchestration & Reasoning
| Component | Technology | Purpose |
|-----------|------------|---------|
| **Orchestrator** | LangGraph | Stateful cyclic graphs for non-linear market analysis and multi-domain routing |
| **Tool I/O** | PydanticAI | Type-safe tool calling, strict JSON validation for strategy genomes and signals |
| **Decision Brain** | DeepSeek-V3 | High-stakes synthesis of the 12 domains in the Decision Domain |
| **Vision Brain** | Gemini 2.5 Flash | Fast chart parsing and structural analysis for the Signal Domain |
| **Document Parser** | LlamaParse / Unstructured | Complex PDF ingestion for the Knowledge Domain |

### 5.2 Data & Infrastructure
| Component | Technology | Purpose |
|-----------|------------|---------|
| **Language** | Python 3.11+ | Backend, ML, strategy compilation, execution logic |
| **Memory/State** | Redis | Real-time tick data, order book state, rate limiting |
| **Database** | PostgreSQL + TimescaleDB | Historical tick data, Trade Journals, Memory Domain |
| **Vector Storage** | Pinecone / Qdrant | Semantic retrieval for the Knowledge Domain |
| **API Gateway** | FastAPI | Webhook ingestion (TV Bot Layer), REST API for Standalone UI |

### 5.3 Execution & Market Data
| Component | Technology | Purpose |
|-----------|------------|---------|
| **Brokerage (Direct)** | IBKR API / CCXT | Multi-asset order routing and position management |
| **Brokerage (MT5)** | MetaTrader 5 API / MQL5 | MT5 EA execution spine, Prop Firm mode enforcement |
| **Order Book Data** | Bookmap API / Rithmic | Level 2 / Heatmap data for the Truth Domain |
| **Options Data** | Unusual Whales API | Institutional flow and dark pool prints |
| **Market Data** | Polygon.io | Low-latency price feeds |
| **Charting UI** | Lightweight Charts (TradingView) | Frontend rendering for the Visual Overlay Domain |

---

## 6. Implementation Instructions for CodeSpring

This section outlines the exact steps to build the LEVIATHAN AI organism. CodeSpring must follow these phases strictly.

### Phase 1: Core Infrastructure & Knowledge Domain
1. **Setup Environment**: Initialize Python 3.11, FastAPI, PostgreSQL, Redis, and Pinecone.
2. **Knowledge Ingestion**: Implement LlamaParse to ingest PDFs and strategy manuals.
3. **Knowledge Structuring**: Build the logic to chunk, classify, and embed trading concepts into Pinecone.
4. **Strategy Genome Schema**: Define the 40+ field Pydantic model for the `StrategyGenome`.

### Phase 2: Signal, Session, and Range Domains
1. **TV Bot Layer**: Implement FastAPI webhooks to receive TradingView alerts.
2. **Signal Domain**: Build the market structure interpreter (MSB/BOS) using incoming price data.
3. **Session & Range Trackers**: Implement background workers (Redis-backed) to continuously track PDH, PDL, overnight ranges, and active sessions (Asian, London, NY).

### Phase 3: The Truth Domain (Data Pipelines)
1. **Level 2 Ingestion**: Connect to Rithmic/Bookmap APIs via WebSockets to track bid/ask imbalance and spoofing.
2. **Options Flow**: Connect to Unusual Whales API to track institutional sweeps.
3. **State Engine**: Implement the logic to classify the current market state (compression, expansion, etc.) based on Phase 2 and 3 data.

### Phase 4: Decision & Risk Governance
1. **Risk Engine (Sovereign)**: Hard-code the risk limits (max daily drawdown, position sizing, prop firm rules). This module must wrap all execution calls.
2. **Decision Engine**: Implement LangGraph to route data from all previous domains into DeepSeek-V3 for the final "approve/reject/wait" output.

### Phase 5: Execution Spines & Visual Overlay
1. **Direct Broker**: Implement CCXT/IBKR integration for bracket orders and routing.
2. **MT5 EA**: Generate the MQL5 Expert Advisor template that listens to ORACLE's Python backend and enforces Prop Firm rules locally.
3. **Visual Overlay**: Build the React/Next.js frontend using Lightweight Charts, overlaying the Level 2 heatmap and AI confidence markers on top of the price action.

### Phase 6: Memory & Evolution
1. **Trade Journal**: Implement the PostgreSQL schema to log every setup, decision, MAE, MFE, and outcome.
2. **Drift Detection**: Build the cron job that analyzes the Trade Journal to demote or retire failing strategies automatically.

---

## 7. Transferable Architecture from Claude Code Source

> **CRITICAL**: Before building any domain, CodeSpring MUST read [`docs/claude-code-transferable-architecture.md`](docs/claude-code-transferable-architecture.md).

This document maps 14 battle-tested architectural patterns from the most sophisticated production AI agent (Claude Code, reverse-engineered at [claude-code-from-source.com](https://claude-code-from-source.com/)) directly to ORACLE's trading domains. These are not theoretical — they are proven patterns running at scale.

### 7.1 Priority 0 (Must Implement First — Prevents Catastrophic Failures)

| Pattern | ORACLE Application |
|---------|--------------------|
| **Permission Mode System** | ORACLE's 7 operating modes (Research, Advisory, Semi-Auto, Full Auto, Prop Firm, Recovery, Signal-Only) become named permission modes that control execution capability |
| **Snapshot Security** | Risk parameters (drawdown limits, position sizing, prop firm thresholds) frozen at session start — no runtime self-modification |
| **Hook System (PreTradeSubmit)** | Risk Governance implemented as lifecycle hooks with exit-code-2 blocking, not a monolithic function |

### 7.2 Priority 1 (Core Functionality)

| Pattern | ORACLE Application |
|---------|--------------------|
| **Async Generator Loop** | The 14-step Live Market Flow as an async generator yielding DomainSignal objects with 8 typed terminal states |
| **Stop Hook (Trade Verification)** | Verification loop before execution — re-checks Truth Domain, risk limits, spread, prop firm compliance |
| **Sub-Agent Pattern** | Each domain as a sub-agent with its own context, tools, and permission scope |
| **Memory System (4-Type Taxonomy)** | Trade memories classified as Trader Profile, Trade Corrections, Active Campaigns, Market Bookmarks |

### 7.3 Priority 2 (Performance Optimization)

| Pattern | ORACLE Application |
|---------|--------------------|
| **Fork Agent (Parallel Analysis)** | Session, Range, State, and Liquidity domains run in parallel sharing 99%+ prompt prefix — 4x cost reduction |
| **4-Layer Context Compression** | Tick budget → Signal snip → Session compact → History collapse prevents context overflow |
| **Two-Tier State** | Infrastructure state (positions, P&L) separated from reactive UI state (signals, overlays) |
| **Bootstrap Pipeline** | Market-open readiness in ~1.25 seconds across 5 phases |

### 7.4 Priority 3 (Long-Term Learning)

| Pattern | ORACLE Application |
|---------|--------------------|
| **Staleness System** | Strategy Genomes get age warnings forcing re-validation through Research Domain |
| **Background Extraction Agent** | Post-trade forked agent catches lessons the main system missed |

### 7.5 AI-Systematic Strategy Pipeline (Research → Backtest → Iterate → Implement)

All Claude Code patterns are integrated within ORACLE's original 4-layer framework:

| Layer | Purpose | Claude Patterns Applied |
|-------|---------|------------------------|
| **1. Research** | Gather market data, sentiment, liquidity | Sub-Agent isolation, Context Compression, Fork Agents for parallel data |
| **2. Backtest** | Test strategies against historical data | ULTRAPLAN (30-min cloud planning), Fork Agents for Monte Carlo, Self-Describing Tools |
| **3. Iterate** | Learn from results, prune failures | KAIROS (always-on logging), Staleness warnings, /dream consolidation, Background Extraction |
| **4. Implement** | Execute in live markets | Async Generator Loop, Stop Hooks, Snapshot Security, 7 Permission Modes |

**Strategy Filtering Pipeline**: Strategies pass through 8 filter stages across Layers 2-4 (Initial Generation → Monte Carlo → Walk-Forward → Regime Testing → Staleness Check → Memory Cross-Reference → Paper Trade → Full Deployment). Approximately 2-3% of generated strategies survive to live deployment.

**Automated Implementation**: Surviving strategies are auto-generated as MT5 EAs or Pine Scripts, deployed in Semi-Auto mode, promoted to Full Auto after 10 matching trades, and auto-demoted if performance deviates by >2σ from backtest expectations.

### 7.6 Hidden Features from Claude Code Leak

| Feature | ORACLE Application |
|---------|--------------------|
| **ULTRAPLAN** | Cloud-based Opus session generates strategy genomes with 30-minute budget and browser approval |
| **KAIROS** | Always-on market monitoring with append-only daily logs and proactive pattern detection |
| **Coordinator Mode** | 370-line system prompt orchestrating all 12 domains with "never delegate understanding" rule |
| **Claude Mythos / Capybara** | Next-gen model tier for maximum reasoning capability when available |
| **DAEMON Mode** | Background process for continuous market monitoring outside trading hours |

Full implementation details, code examples, the complete AI-systematic pipeline, and rationale for each pattern are in [`docs/claude-code-transferable-architecture.md`](docs/claude-code-transferable-architecture.md).
