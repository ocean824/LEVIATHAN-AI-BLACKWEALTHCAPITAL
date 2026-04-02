# ORACLE AI: Advanced Order Flow & Intelligence Trading System

> **Organization:** Black Wealth Capital
> **Project:** ORACLE AI — Standalone Trading Software & Intelligence Core
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

ORACLE AI is the trading mind of Black Wealth Capital. It is designed as a standalone, institutionally structured, research-first trading organism. 

Its identity is not built around "prediction" — its identity is built around **capital permission**. It exists to absorb trading knowledge, transform that knowledge into structured strategy intelligence, read live markets across multiple truth layers, and decide whether capital deserves deployment.

### The 6 Core Principles
1. **Research comes before deployment**: No setup becomes live logic merely because it looks good. It must be structured, tested, and validated.
2. **Market state comes before chart pattern**: A pattern's value depends on session, prior range, volatility, and liquidity context.
3. **Order book truth outranks chart cosmetics**: If level-two flow and liquidity behavior contradict the chart, ORACLE must downgrade or reject the idea.
4. **Risk is sovereign**: Risk governance is its own authority. Nothing else may override it.
5. **Execution is part of the edge**: Trade management (entry, slippage, scaling, exits) is part of the strategy, not a separate convenience.
6. **Knowledge must be ingested, but never worshipped**: Documents and books are inputs. They must be parsed, validated, and tested through research before influencing real capital.

---

## The 12+ Domain Architecture

ORACLE AI is not a simple signal bot. It is an organism built from tightly connected domains that handle everything from document parsing to direct broker execution.

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
The chart-to-intelligence bridge. Receives TradingView webhooks, maps them to ORACLE strategy families, enriches with session/state context, passes to Truth Domain for verification, and renders response back to user workflow.

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

---

## Global Tech Stack

ORACLE AI relies on a modern, high-performance tech stack to execute its architecture:

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

ORACLE AI adapts to different environments and risk tolerances:
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

While ORACLE AI is a standalone organism, it connects to the broader ØMEGA AI orchestrator as a specialized peer (the `QUANTUM` Agent). It communicates via a **dedicated status protocol**:
- **Status Heartbeat**: Broadcasts current bias, market regime, and confidence.
- **Inquiry/Response**: ØMEGA sends a signal; ORACLE returns a validated Confidence Score.
- **Kill Switch Sync**: A global halt in either system triggers a halt in the other.

---

## AI-Systematic Strategy Pipeline

ORACLE uses Claude Code's proven architectural patterns as the execution engine for its original 4-layer framework. The AI does not just signal — it researches, backtests, filters, and implements strategies automatically.

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

This repository contains detailed research, architecture, and specification documents. Use the links below to navigate directly to specific areas of the ORACLE AI platform.

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

**ORACLE AI — Built for Black Wealth Capital.**
