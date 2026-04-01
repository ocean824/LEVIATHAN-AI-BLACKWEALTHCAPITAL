# ORACLE AI: Advanced Order Flow & Intelligence Trading System

> **Organization:** Black Wealth Capital
> **Project:** ORACLE AI — Standalone Trading Software & Intelligence Core
> **Status:** Strategic Blueprint / Full System Architecture
> **Last Updated:** April 2026

---

## What Is ORACLE AI?

ORACLE AI is the trading mind of Black Wealth Capital. It is designed as a standalone, institutionally structured, research-first trading organism. 

Its identity is not built around "prediction" — its identity is built around **capital permission**. It exists to absorb trading knowledge, transform that knowledge into structured strategy intelligence, read live markets across multiple truth layers, and decide whether capital deserves deployment.

It functions simultaneously as:
1. **A Standalone Software**: A dedicated trading platform with direct broker/MT5 execution, visual chart overlays, and independent risk governance.
2. **An Intelligence Core**: The primary quantitative trading brain (`QUANTUM` Agent) for the **ØMEGA AI** ecosystem.

---

## 🏗️ The 12+ Domain Architecture

ORACLE AI is not a simple signal bot. It is an organism built from tightly connected domains:

| Domain | Purpose & Capabilities |
|--------|------------------------|
| **1. Knowledge** | Ingests documents (PDFs, manuals), chunks, classifies, and extracts structured strategy components. |
| **2. Research** | The strategy laboratory. Generates Pine Script/Python/MT5 code, tests, and validates strategies before live deployment. |
| **3. Signal** | The chart and structure interpreter. Detects MSB/BOS, trend state, liquidity maps, and patterns. |
| **4. Session** | Treats time-of-day as a first-class edge (Asian, London Open, NY Overlap). |
| **5. Previous Day & Range** | Tracks and interprets PDH, PDL, midpoint, overnight highs/lows, and opening ranges. |
| **6. State** | Treats the market as a state machine (compression, expansion, breakout, exhaustion, reversal). |
| **7. Liquidity** | Quantifies smart money concepts (equal highs/lows, pools, FVGs, sweep/reclaim). |
| **8. Truth** | Validates chart ideas using Level 2 Order Book, options flow, and economic event context. |
| **9. Visual Overlay** | Renders advanced intelligence (liquidity heatmaps, order-book density) over TradingView-style charts. |
| **10. TradingView Bot** | The chart-to-intelligence bridge. Parses webhooks, enriches with context, and verifies via Truth Domain. |
| **11. Decision & Risk** | Determines if capital is justified. **Risk Governance is sovereign** and can veto any trade. |
| **12. Execution & Memory** | Routes via Direct Broker or MT5 EA (with Prop Firm mode). Records every action for self-improvement. |

---

## 💻 Global Tech Stack

ORACLE AI relies on a modern, high-performance tech stack to execute its 12-domain architecture:

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

## 🔄 Integration with ØMEGA AI

While ORACLE AI is a standalone organism, it connects to the broader ØMEGA AI orchestrator as a specialized peer. It communicates via a **dedicated status protocol**:
- **Status Heartbeat**: Broadcasts current bias, market regime, and confidence.
- **Inquiry/Response**: ØMEGA sends a signal; ORACLE returns a validated Confidence Score.
- **Kill Switch Sync**: A global halt in either system triggers a halt in the other.

---

## 🛠️ Repository Structure

```
ORACLE-AI-BLACKWEALTHCAPITAL/
├── README.md                                    ← This file
├── CODESPRING-MASTER-INSTRUCTIONS.md            ← The definitive 12-domain implementation blueprint
├── CODESPRING-INTEGRATION-MANIFEST.md           ← Phase 1 integration targets
├── docs/
│   ├── oracle-full-master-writeup.md            ← The original 1,000+ line system design narrative
│   ├── oracle-trading-system.md                 ← Legacy architectural overview
│   └── protocol-spec.md                         ← Communication with ØMEGA AI
├── architectures/
│   ├── layer1-data-pipeline.md                  ← Tick data & options flow logic
│   └── layer2-vision-analysis.md                ← Chart parsing & visual intelligence
├── prompts/
│   ├── decision-engine-prompt.md                ← Layer 4 synthesis prompt
│   └── alignment-check.md                       ← Final "GO/NO-GO" verification
├── security/
│   ├── capital-preservation-rules.md            ← Hard-coded risk constraints
│   └── api-key-isolation.md                     ← Sandbox & credential security
└── src/                                         ← Source code placeholders
```

---

## 🚀 tldr: Implementation Roadmap for CodeSpring

1. **Ingest `CODESPRING-MASTER-INSTRUCTIONS.md`** — This is the master blueprint containing the full 12-domain architecture, end-to-end workflow, and tech stack.
2. **Phase 1: Knowledge & Research**: Implement the Knowledge Domain (document ingestion via LlamaParse) and Research Domain (strategy genome) to ensure no strategy goes live without validation.
3. **Phase 2: Signal & State**: Build the TV Bot Layer and background workers to track sessions, ranges, and market states.
4. **Phase 3: The Truth Domain**: Connect to Level 2 / Bookmap-style data feeds and Unusual Whales to validate chart signals.
5. **Phase 4: Decision & Risk**: Hard-code the sovereign Risk Engine and implement LangGraph + DeepSeek-V3 for the Decision Engine.
6. **Phase 5: Execution Spines**: Build the dual execution paths — Direct Broker API (CCXT/IBKR) and the MetaTrader 5 Expert Advisor (with built-in Prop Firm mode).
7. **Phase 6: Visual Overlay**: Implement the low-opacity visual overlay for TradingView-style charts using Lightweight Charts.

---

**ORACLE AI — Built for Black Wealth Capital.**
