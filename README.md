# ORACLE AI: Advanced Order Flow & Intelligence Trading System

> **Organization:** Black Wealth Capital
> **Project:** ORACLE AI — Standalone Trading Software & Intelligence Core
> **Status:** Strategic Blueprint / Phase 1: Data Pipeline
> **Last Updated:** March 2026

---

## What Is ORACLE AI?

ORACLE AI is a high-fidelity, multi-layer intelligence system designed for professional trading. It operates on a **4-layer confirmation stack**, moving beyond simple visual analysis to ingest raw tick data, institutional options flow, and indicator states.

It is designed to be:
1. **Standalone Software**: A dedicated trading platform with its own execution and UI.
2. **Intelligence Core**: The primary trading brain for the **ØMEGA AI** ecosystem.

---

## 🏗️ 4-Layer Architecture

| Layer | Component | Source / Tools | Purpose |
|-------|-----------|----------------|---------|
| **Layer 1** | **Data Ingestion** | Unusual Whales, IBKR, Rithmic | Order flow, options flow, institutional bias. |
| **Layer 2** | **Visual Intelligence** | VLM (Vision), Chart OCR | Liquidity sweeps, trend structure, fakeouts. |
| **Layer 3** | **Indicator Engine** | TradingView, PineScript | Structured RSI, MACD, Volume, Session context. |
| **Layer 4** | **Decision Engine** | DeepSeek-V3, PydanticAI | Synthesis of Layers 1-3 into high-confidence bias. |

---

## 🔄 Integration with ØMEGA AI

ORACLE AI is not a replacement for the ØMEGA AI orchestrator; it is a specialized peer. It communicates via a **dedicated status protocol**:
- **Confidence Scores**: Returns a percentage (0-100%) for any given trade signal.
- **Kill Switch Sync**: Global halt in either system triggers a halt in the other.
- **Knowledge Sharing**: Feeds discovered market regimes to the Research agent.

---

## 🛠️ Repository Structure

```
ORACLE-AI-BLACKWEALTHCAPITAL/
├── README.md                                    ← This file
├── CODESPRING-INTEGRATION-MANIFEST.md           ← Blueprint for CodeSpring
├── docs/
│   ├── oracle-trading-system.md                 ← Master architectural blueprint
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
    └── layers/                                  ← Layer 1-4 implementations
```

---

## 🚀 tldr: Quick Start for CodeSpring

1. **Ingest the `docs/oracle-trading-system.md`** for the core logic.
2. **Phase 1 Priority**: Connect to the **Unusual Whales API** and set up the **TradingView webhook listener**.
3. **Layer 4 Target**: Implement the synthesis logic that requires alignment across all three lower layers before outputting a bias.
4. **Standalone UI**: Start with a basic dashboard for real-time confidence scores and order flow visualization.

---

**ORACLE AI — Built for Black Wealth Capital.**
