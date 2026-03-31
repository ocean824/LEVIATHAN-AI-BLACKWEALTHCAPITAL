# 🔮 CODESPRING MASTER INSTRUCTIONS: ORACLE AI (BLACK WEALTH CAPITAL)

> **Role**: Lead Quantitative Developer & Systems Architect
> **Objective**: Implement the ORACLE AI Standalone Trading System.
> **Status**: Hyper-Detailed Implementation Blueprint (Institutional-Grade)

---

## 1. System Identity & Mission
ORACLE AI is a **high-fidelity, multi-layer intelligence system** designed for professional trading. It is the **intelligence core** of the ØMEGA AI ecosystem.

### 1.1 Tech Stack (Mandatory)
- **Language**: Python 3.11+.
- **Data Ingestion**: Unusual Whales API, IBKR, Rithmic (futures tick data).
- **Visual Intelligence**: Multimodal LLM (Vision) for chart analysis.
- **Orchestration**: PydanticAI (Type-safe validation).
- **Reasoning Engine**: DeepSeek-V3 (High-stakes decision logic).

---

## 2. The 4-Layer Confirmation Stack (Logic & Tools)

### 2.1 Layer 1: Real Data (Order Flow & Options)
**Logic**: Ingest institutional options flow (Unusual Whales) and futures tick data.
- **Tools**: Unusual Whales API, Polygon.io, IBKR API.
- **Goal**: Detect institutional bias, aggressive market participation, and liquidity walls.

### 2.2 Layer 2: Visual Intelligence (Vision)
**Logic**: Take live TradingView chart screenshots and analyze for:
- **Trend Structure**: MSB (Market Structure Break) / BOS (Break of Structure).
- **Liquidity**: Liquidity sweeps, equal highs/lows.
- **Confirmation**: Fakeouts vs. Breakouts.
- **Tools**: Multimodal LLMs (Vision), OCR parsing.

### 2.3 Layer 3: Indicator State (Structured)
**Logic**: Ingest raw values (RSI, MACD, EMA) via TradingView webhooks.
- **Goal**: Provide the "mathematical truth" to the decision engine.
- **Requirement**: No screenshots for indicators—must be structured data.

### 2.4 Layer 4: Decision Engine (Synthesis)
**Logic**: The "Alignment Gate." 
- **Constraint**: **Layer 1 + Layer 3 must align** before Layer 4 triggers.
- **Output**: Bias (Long/Short), Confidence Score (0-100%), Entry/Stop/Target.

---

## 3. Communication Protocol (Oracle <-> ØMEGA AI)
Oracle must implement a **REST API** or **WebSocket** for ØMEGA AI to:
1. **Request Confidence Score**: Omega sends a signal; Oracle returns a score.
2. **Status Heartbeat**: Oracle reports market regime (Chop/Trend) and operational health.
3. **Kill Switch Sync**: Immediate halt in either system triggers a halt in the other.

---

## 4. Security & Risk Governance (Hard-Coded)
- **Rule 1**: Max daily loss limit (Hard-coded).
- **Rule 2**: No trade can be executed without a Confidence Score > 75%.
- **Rule 3**: All API keys must be isolated in a secure vault/sandbox.

---

## 5. Tool & API Schema (Pydantic)
```python
from pydantic import BaseModel, Field

class TradeSignal(BaseModel):
    bias: str = Field(enum=["LONG", "SHORT", "NEUTRAL"])
    confidence_score: float = Field(ge=0.0, le=1.0)
    entry_price: float
    stop_loss: float
    take_profit: list[float]
    reasoning: str = Field(description="The multi-layer confirmation logic.")
```

---

## 6. Implementation Roadmap for CodeSpring
1. **Phase 1**: Connect to the **Unusual Whales API** and implement the data normalizer.
2. **Phase 2**: Set up the **Vision analysis loop** for TradingView screenshots.
3. **Phase 3**: Build the **Layer 4 Synthesis Engine** using PydanticAI.
4. **Phase 4**: Implement the **ØMEGA AI Status Protocol** and Standalone UI.

---
**BLACK WEALTH CAPITAL — ORACLE AI — THE INTELLIGENCE CORE.**
