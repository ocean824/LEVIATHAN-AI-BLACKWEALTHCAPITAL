# CODESPRING INTEGRATION MANIFEST: ORACLE AI

> **To CodeSpring Orchestrator:** This document is the primary entry point for the implementation of the **ORACLE AI** (Black Wealth Capital). It maps the high-level trading research to specific implementation targets for this standalone software.

---

## 1. Project Identity & Context
- **Project Name**: ORACLE AI (Black Wealth Capital)
- **Architecture**: 4-Layer Confirmation Stack.
- **Primary Goal**: High-probability trading decision quality through stacked confirmation.
- **Core Methodology**: Order Flow (Layer 1), Visual AI (Layer 2), Indicator State (Layer 3), Synthesis (Layer 4).

---

## 2. Implementation Priorities (Phase 1)

### 2.1 Layer 1: Data Pipeline
- **Source**: `docs/oracle-trading-system.md`
- **Task**: Connect to the **Unusual Whales API** for options sentiment and institutional sweeps.
- **Logic**: Ingest real-time data and normalize it into a structured JSON format for Layer 4.

### 2.2 Layer 2: Visual Intelligence
- **Source**: `docs/oracle-trading-system.md`
- **Task**: Set up a **Vision analysis loop** for chart screenshots (TradingView).
- **Tooling**: Multimodal LLM (Vision) to detect trend structure, liquidity sweeps, and fakeouts.

### 2.3 Layer 3: Indicator State Engine
- **Source**: `docs/oracle-trading-system.md`
- **Task**: Implement a **Webhook listener** for structured indicator data (RSI, MACD, Volume).
- **Logic**: Hard-coded constraints that provide the "mathematical truth" to the decision engine.

### 2.4 Layer 4: Decision Engine (Synthesis)
- **Source**: `docs/oracle-trading-system.md`
- **Task**: Implement the final synthesis logic that answers: *"Are all systems aligned right now?"*
- **Output**: Bias (Long/Short), Confidence Score (%), Entry/Stop/Target.

---

## 3. Communication Protocol (Oracle <-> ØMEGA AI)
- **Source**: `docs/protocol-spec.md`
- **Task**: Implement the **Status Heartbeat** and **Inquiry/Response** logic.
- **Requirement**: Standardize the communication so ØMEGA AI can "ask" Oracle for a confidence score on any signal.

---

## 4. Security & Risk
- **Source**: `security/capital-preservation-rules.md`
- **Implementation**: Hard-coded risk constraints (Max drawdown, daily loss limit).
- **Gatekeeper**: No trade can be executed without Layer 4's "GO" signal AND risk manager approval.

---

## 5. Instructions for CodeSpring
1. **Ingest the `docs/` folder** first to understand the trading-specific logic.
2. **Prioritize Layer 1 and Layer 4** as the foundational logic for the standalone engine.
3. **Use DeepSeek-V3** as the primary reasoning engine for all high-stakes trading decisions.
4. **Standalone UI**: Implement a dashboard for real-time confidence scores and order flow visualization.

---

**ORACLE AI — Built for Black Wealth Capital.**
