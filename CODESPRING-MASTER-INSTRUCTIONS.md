# CODESPRING MASTER INSTRUCTIONS: ORACLE AI (Black Wealth Capital)

> **Role**: Lead Quantitative Developer & Systems Architect
> **Objective**: Implement the ORACLE AI Standalone Trading System.
> **Status**: Implementation-Ready (Zero-Question Blueprint)

---

## 1. System Identity & Identity
ORACLE AI is a **standalone, multi-layer intelligence system** designed for high-probability trade decision quality.

### 1.1 Tech Stack (Mandatory)
- **Language**: Python 3.11+.
- **Data Ingestion**: Unusual Whales API, IBKR, Rithmic.
- **Visual Intelligence**: Multimodal LLM (Vision) for chart analysis.
- **Orchestration**: PydanticAI (Type-safe validation).
- **Reasoning Engine**: DeepSeek-V3 (High-stakes decision logic).

---

## 2. 4-Layer Confirmation Logic

### 2.1 Layer 1: Real Data (Order Flow)
- **Logic**: Ingest institutional options flow (Unusual Whales) and futures tick data.
- **Goal**: Detect institutional bias and aggressive market participation.

### 2.2 Layer 2: Visual Intelligence (Vision)
- **Logic**: Take live TradingView chart screenshots and analyze for:
    - Liquidity sweeps.
    - Trend structure (MSB/BOS).
    - Fakeouts vs. Breakouts.

### 2.3 Layer 3: Indicator State (Structured)
- **Logic**: Ingest raw values (RSI, MACD, EMA) via TradingView webhooks.
- **Goal**: Provide the "mathematical truth" to the decision engine.

### 2.4 Layer 4: Decision Engine (Synthesis)
- **Logic**: The "Alignment Gate." 
- **Requirement**: **Layer 1 + Layer 3 must align** before Layer 4 triggers.
- **Output**: Bias (Long/Short), Confidence Score (0-100%), Entry/Stop/Target.

---

## 3. Communication Protocol (Oracle <-> ØMEGA AI)
Oracle must implement a **REST API** or **WebSocket** for ØMEGA AI to:
1. **Request Confidence Score**: Omega sends a signal; Oracle returns a score.
2. **Status Heartbeat**: Oracle reports market regime (Chop/Trend) and operational health.
3. **Kill Switch Sync**: Immediate halt in either system triggers a halt in the other.

---

## 4. Security & Risk Governance
- **Rule 1**: Max daily loss limit (Hard-coded).
- **Rule 2**: No trade can be executed without a Confidence Score > 75%.
- **Rule 3**: All API keys must be isolated in a secure vault/sandbox.

---

## 5. Implementation Roadmap
1. **Phase 1**: Connect to the **Unusual Whales API** and implement the data normalizer.
2. **Phase 2**: Set up the **Vision analysis loop** for TradingView screenshots.
3. **Phase 3**: Build the **Layer 4 Synthesis Engine** using PydanticAI.
4. **Phase 4**: Implement the **ØMEGA AI Status Protocol**.

---

## 6. Reference Documentation
- **Master Blueprint**: `docs/oracle-trading-system.md`
- **Protocol Spec**: `docs/protocol-spec.md`
- **Security Rules**: `security/capital-preservation-rules.md`

---
**BLACK WEALTH CAPITAL — ORACLE AI — THE INTELLIGENCE CORE.**
