# LEVIATHAN AI Schema Contracts and Example Payloads

**Status:** Additive pre-handoff implementation appendix  
**Purpose:** Convert the LEVIATHAN AI architecture into a stricter set of executable object contracts for CodeSpring implementation

## Why This Document Exists

LEVIATHAN AI already defines a sophisticated trading organism across research, signal intake, state interpretation, truth validation, decisioning, risk governance, execution, and memory.[1] [2] The remaining implementation gap is that many of those layers are described conceptually rather than encoded as a canonical set of payload contracts. This document closes that gap by defining the minimum typed objects CodeSpring should treat as the first stable surface of the system.[1] [2] [3]

The goal is not to freeze every future evolution. The goal is to provide a **clean first contract layer** so that ingestion, replay, testing, and execution all talk about the same objects.

## Canonical Layer-1 Object Set

| Object | Layer Owner | Purpose |
|---|---|---|
| **StrategyGenome** | Research Domain | Stores the validated trading doctrine and deployment constraints for a strategy family |
| **CandidateSetup** | Signal / Session / State | Represents a possible trade opportunity entering the ORACLE pipeline |
| **TruthValidationResult** | Truth Domain | Captures confirmation or rejection from order-flow, event-risk, and external truth layers |
| **DecisionPacket** | Decision Domain | Encodes the system’s approved, rejected, or deferred decision |
| **RiskSnapshot** | Sovereign Risk Engine | Freezes current risk conditions so execution cannot improvise its own thesis |
| **ExecutionIntent** | Execution Layer | Specifies the trade plan that may be routed into paper simulation or live execution |
| **TradeJournalRecord** | Memory / Review | Stores the replayable post-trade record |

## Pydantic Reference Models

The following example models are deliberately minimal. They are intended as the first real contract layer, not as the final full production schema.

```python
from datetime import datetime, UTC
from typing import Literal
from uuid import uuid4
from pydantic import BaseModel, Field


class StrategyGenome(BaseModel):
    strategy_id: str
    family: str
    market: str
    timeframe: str
    session_dependencies: list[str] = Field(default_factory=list)
    state_dependencies: list[str] = Field(default_factory=list)
    entry_conditions: list[str] = Field(default_factory=list)
    exit_conditions: list[str] = Field(default_factory=list)
    risk_profile: str
    failure_modes: list[str] = Field(default_factory=list)
    prop_firm_compatible: bool = True


class CandidateSetup(BaseModel):
    setup_id: str
    instrument: str
    timestamp: str
    signal_features: list[str] = Field(default_factory=list)
    session_label: str | None = None
    range_label: str | None = None
    state_label: str | None = None
    liquidity_features: list[str] = Field(default_factory=list)


class TruthValidationResult(BaseModel):
    setup_id: str
    orderbook_bias: Literal["bullish", "bearish", "neutral"]
    options_context: str
    event_risk: Literal["safe", "reduced_risk", "no_trade"]
    sentiment_modifier: float
    truth_status: Literal["confirmed", "mixed", "rejected"]
    notes: str


class DecisionPacket(BaseModel):
    decision_id: str
    setup_id: str
    permission: Literal["reject", "wait", "approve", "signal_only"]
    direction: Literal["long", "short", "flat"]
    confidence: float
    entry_style: str
    scaling_allowed: bool
    justification: str


class RiskSnapshot(BaseModel):
    session_id: str
    max_daily_drawdown: float
    max_position_size: float
    allowed_instruments: list[str]
    prop_firm_rules: list[str]
    frozen_at: str


class ExecutionIntent(BaseModel):
    decision_id: str
    broker_path: Literal["paper_sim", "mt5", "direct_broker"]
    order_type: Literal["market", "limit", "stop"]
    size: float
    stop_loss: float
    take_profit: float
    time_in_force: Literal["DAY", "GTC"]


class TradeJournalRecord(BaseModel):
    trade_id: str
    setup_id: str
    decision_id: str
    entry: float
    exit: float
    mae: float
    mfe: float
    outcome: Literal["win", "loss", "scratch", "blocked"]
    post_trade_notes: str
```

## Example Layer-1 Payload Pack

These example payloads show what a first end-to-end paper-trade cycle should look like if the contracts above are respected.

### StrategyGenome Example

```json
{
  "strategy_id": "genome_nq_opening_range_break_v1",
  "family": "opening_range_break",
  "market": "NQ",
  "timeframe": "1m-5m",
  "session_dependencies": ["ny_open"],
  "state_dependencies": ["breakout", "trend_continuation"],
  "entry_conditions": [
    "opening range defined",
    "structure break above opening range high",
    "liquidity sweep complete"
  ],
  "exit_conditions": [
    "2R achieved",
    "failed acceptance back inside range",
    "macro event invalidation"
  ],
  "risk_profile": "moderate_intraday",
  "failure_modes": ["fake breakout", "news reversal", "thin liquidity continuation trap"],
  "prop_firm_compatible": true
}
```

### CandidateSetup Example

```json
{
  "setup_id": "setup_6fc2a3d4c211",
  "instrument": "NQ",
  "timestamp": "2026-04-15T14:35:00Z",
  "signal_features": ["msb_up", "opening_range_break", "ema_alignment"],
  "session_label": "ny_open",
  "range_label": "above_opening_range_high",
  "state_label": "breakout",
  "liquidity_features": ["equal_highs_swept", "inefficiency_below"]
}
```

### TruthValidationResult Example

```json
{
  "setup_id": "setup_6fc2a3d4c211",
  "orderbook_bias": "bullish",
  "options_context": "No large bearish sweep detected in near-dated contracts.",
  "event_risk": "safe",
  "sentiment_modifier": 0.07,
  "truth_status": "confirmed",
  "notes": "Aggressive buyers lifted the offer after the sweep and accepted above the opening range high."
}
```

### DecisionPacket Example

```json
{
  "decision_id": "dec_78cd20a4f5aa",
  "setup_id": "setup_6fc2a3d4c211",
  "permission": "approve",
  "direction": "long",
  "confidence": 0.74,
  "entry_style": "breakout_retest",
  "scaling_allowed": true,
  "justification": "Signal, state, and truth layers are aligned with no current macro veto."
}
```

### RiskSnapshot Example

```json
{
  "session_id": "session_8a20d88fbc",
  "max_daily_drawdown": 1.5,
  "max_position_size": 0.25,
  "allowed_instruments": ["NQ"],
  "prop_firm_rules": ["daily_dd_lock", "loss_streak_throttle", "no_overnight_hold"],
  "frozen_at": "2026-04-15T14:35:01Z"
}
```

### ExecutionIntent Example

```json
{
  "decision_id": "dec_78cd20a4f5aa",
  "broker_path": "paper_sim",
  "order_type": "limit",
  "size": 0.1,
  "stop_loss": 18240.0,
  "take_profit": 18270.0,
  "time_in_force": "DAY"
}
```

### TradeJournalRecord Example

```json
{
  "trade_id": "trade_2bc44d781e2c",
  "setup_id": "setup_6fc2a3d4c211",
  "decision_id": "dec_78cd20a4f5aa",
  "entry": 18250.0,
  "exit": 18268.0,
  "mae": -3.0,
  "mfe": 18.0,
  "outcome": "win",
  "post_trade_notes": "Paper-trade replay completed with orderly retest confirmation and no risk veto."
}
```

## Contract Rules That Should Be Enforced

| Rule | Reason |
|---|---|
| **Execution may not create its own thesis** | Prevents execution from bypassing decision and risk layers |
| **Decision may not ignore Truth status** | Preserves the architecture’s validation discipline |
| **RiskSnapshot must be frozen before ExecutionIntent exists** | Avoids moving risk goalposts mid-trade |
| **Every completed trade must end in a TradeJournalRecord** | Makes replay and improvement possible |
| **Every blocked trade should still be journaled** | Prevents hidden failure modes |

## Example Validation Helpers

```python
def assert_trade_is_executable(decision: DecisionPacket, risk: RiskSnapshot, instrument: str) -> None:
    if decision.permission != "approve":
        raise ValueError("Trade is not approved for execution")
    if instrument not in risk.allowed_instruments:
        raise ValueError(f"Instrument {instrument} is not allowed under current risk rules")


def create_execution_intent(decision: DecisionPacket, risk: RiskSnapshot, entry_price: float) -> ExecutionIntent:
    assert_trade_is_executable(decision, risk, instrument="NQ")
    return ExecutionIntent(
        decision_id=decision.decision_id,
        broker_path="paper_sim",
        order_type="limit",
        size=min(0.10, risk.max_position_size),
        stop_loss=entry_price - 10.0,
        take_profit=entry_price + 20.0,
        time_in_force="DAY",
    )
```

## Recommended File Path Mapping

A straightforward implementation layout for these objects would be the following.

| Proposed Path | Purpose |
|---|---|
| `src/oracle/schemas/strategy.py` | StrategyGenome and research models |
| `src/oracle/schemas/setup.py` | CandidateSetup and ingress payloads |
| `src/oracle/schemas/truth.py` | TruthValidationResult and truth-source contracts |
| `src/oracle/schemas/decision.py` | DecisionPacket and policy decisions |
| `src/oracle/schemas/risk.py` | RiskSnapshot and prop-firm restrictions |
| `src/oracle/schemas/execution.py` | ExecutionIntent and broker routing contracts |
| `src/oracle/schemas/journal.py` | TradeJournalRecord and replay history |

## TL;DR

If CodeSpring receives only one new ORACLE appendix before implementation, it should be this one. The system becomes much easier to build once **every layer speaks in a strict shared object vocabulary**.

## References

[1]: ../README.md "LEVIATHAN AI README"
[2]: ./claude-code-transferable-architecture.md "ORACLE Claude Code Transferable Architecture"
[3]: ./additive-implementation-priorities.md "LEVIATHAN AI Additive Implementation Priorities"
