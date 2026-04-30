# LEVIATHAN AI Additive Implementation Priorities

**Status:** Additive implementation note  
**Intent:** Preserve the existing LEVIATHAN AI architecture while defining the smallest high-leverage next steps toward execution

## Why This Document Exists

LEVIATHAN AI already has strong conceptual separation across research, signal interpretation, session and range context, state modeling, liquidity, truth validation, decisioning, sovereign risk governance, execution, position management, and memory.[1] [2] What it needs next is not a new philosophy. It needs a narrow set of implementation contracts that can prove the architecture under simulation and then under controlled execution.[1] [2]

This note is intentionally **additive**. It does not replace any architecture file or master instruction set.

## Implementation Principle

The best ORACLE build path is to encode the system in layers exactly as the repository already describes it: **Research → Backtest → Iterate → Implement**.[2] Any shortcut that jumps directly from idea generation into broker execution would violate the system’s own design logic.[1] [2]

| Priority Tier | Objective | Why |
|---|---|---|
| **P0** | Freeze the core trading schemas | Prevent logic drift between research, decision, risk, and execution |
| **P1** | Build one replayable paper-trading slice | Prove the 14-step flow without live capital |
| **P2** | Add drift detection and review tooling | Make learning measurable rather than rhetorical |
| **P3** | Expand data sources and broker integrations | Only after the core loop is auditable |

## P0: Core Schemas That Should Exist in Code

The single highest-value additive move is to encode the central ORACLE concepts as strict models.

| Schema | Minimum Required Fields | Why It Matters |
|---|---|---|
| **Strategy Genome** | `strategy_id`, `family`, `market`, `timeframe`, `session_dependencies`, `state_dependencies`, `entry_conditions`, `exit_conditions`, `risk_profile`, `failure_modes`, `prop_firm_compatible` | Preserves the repository’s research-first doctrine |
| **Candidate Setup** | `setup_id`, `instrument`, `timestamp`, `signal_features`, `session_label`, `range_label`, `state_label`, `liquidity_features` | Standardizes what the signal layer produces |
| **Truth Validation Result** | `setup_id`, `orderbook_bias`, `options_context`, `event_risk`, `sentiment_modifier`, `truth_status`, `notes` | Keeps chart-side ideas separate from market confirmation |
| **Decision Packet** | `decision_id`, `setup_id`, `permission`, `direction`, `confidence`, `entry_style`, `scaling_allowed`, `justification` | Makes the decision layer explicit and replayable |
| **Risk Snapshot** | `session_id`, `max_daily_drawdown`, `max_position_size`, `allowed_instruments`, `prop_firm_rules`, `frozen_at` | Enforces sovereign risk at runtime |
| **Execution Intent** | `decision_id`, `broker_path`, `order_type`, `size`, `stop_loss`, `take_profit`, `time_in_force` | Separates trade planning from actual order placement |
| **Trade Journal Record** | `trade_id`, `setup_id`, `decision_id`, `entry`, `exit`, `mae`, `mfe`, `outcome`, `post_trade_notes` | Enables replay, review, and drift analysis |

## P1: The First Replayable Vertical Slice

ORACLE should first prove itself in a single end-to-end simulated or paper-trading flow. The goal is not to support every domain at once. The goal is to verify that the architecture behaves correctly when one structured signal passes through all required gates.

| Step | Layer / Domain | Output |
|---|---|---|
| 1 | TradingView Bot or mock signal ingress | Candidate Setup |
| 2 | Session / Range / State enrichment | Contextualized setup |
| 3 | Liquidity + Truth validation | Truth Validation Result |
| 4 | Decision engine | Decision Packet |
| 5 | Risk governance | Approved or vetoed execution intent |
| 6 | Simulated execution path | Replayable trade lifecycle |
| 7 | Memory and journal write | Trade Journal Record |
| 8 | Post-trade analysis | Lesson or drift signal |

If ORACLE cannot reliably execute this thin slice in replayable form, then adding more domains or broker paths will only increase fragility.

## First-Layer Code Examples

The first working ORACLE layer should be a **paper-trading decision pipeline**. The point is to make the architecture executable without live capital. These functions represent the minimum meaningful flow.

| Function | Layer-1 Responsibility |
|---|---|
| `ingest_candidate_setup()` | Accept the initial signal payload |
| `enrich_market_context()` | Add session, range, and state labels |
| `validate_truth()` | Perform bounded truth checks |
| `decide_permission()` | Produce a typed decision packet |
| `freeze_risk_snapshot()` | Lock runtime risk parameters |
| `build_execution_intent()` | Prepare a non-live execution plan |
| `journal_trade()` | Record the replayable result |

### Example: Shared Models

```python
from datetime import datetime, UTC
from typing import Literal
from uuid import uuid4
from pydantic import BaseModel, Field


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

### Example: `ingest_candidate_setup()`

```python
def ingest_candidate_setup(instrument: str, signal_features: list[str]) -> CandidateSetup:
    return CandidateSetup(
        setup_id=f"setup_{uuid4().hex[:12]}",
        instrument=instrument,
        timestamp=datetime.now(UTC).isoformat(),
        signal_features=signal_features,
    )
```

### Example: `enrich_market_context()`

```python
def enrich_market_context(setup: CandidateSetup, session_label: str, range_label: str, state_label: str) -> CandidateSetup:
    setup.session_label = session_label
    setup.range_label = range_label
    setup.state_label = state_label
    setup.liquidity_features = ["equal_highs_nearby", "untapped_gap_below"]
    return setup
```

### Example: `validate_truth()`

```python
def validate_truth(setup: CandidateSetup) -> TruthValidationResult:
    truth_status = "confirmed" if setup.state_label in {"expansion", "breakout"} else "mixed"
    return TruthValidationResult(
        setup_id=setup.setup_id,
        orderbook_bias="bullish",
        options_context="No conflicting options sweep detected",
        event_risk="safe",
        sentiment_modifier=0.05,
        truth_status=truth_status,
        notes="Order-book pressure supports the chart-side bias",
    )
```

### Example: `decide_permission()`

```python
def decide_permission(setup: CandidateSetup, truth: TruthValidationResult) -> DecisionPacket:
    if truth.event_risk == "no_trade" or truth.truth_status == "rejected":
        return DecisionPacket(
            decision_id=f"dec_{uuid4().hex[:12]}",
            setup_id=setup.setup_id,
            permission="reject",
            direction="flat",
            confidence=0.0,
            entry_style="none",
            scaling_allowed=False,
            justification="Truth layer or event risk invalidated the setup",
        )

    return DecisionPacket(
        decision_id=f"dec_{uuid4().hex[:12]}",
        setup_id=setup.setup_id,
        permission="approve",
        direction="long",
        confidence=0.74,
        entry_style="breakout_retest",
        scaling_allowed=True,
        justification="Session, state, and truth layers are aligned",
    )
```

### Example: `freeze_risk_snapshot()`

```python
def freeze_risk_snapshot(instrument: str) -> RiskSnapshot:
    return RiskSnapshot(
        session_id=f"session_{uuid4().hex[:10]}",
        max_daily_drawdown=1.5,
        max_position_size=0.25,
        allowed_instruments=[instrument],
        prop_firm_rules=["daily_dd_lock", "loss_streak_throttle"],
        frozen_at=datetime.now(UTC).isoformat(),
    )
```

### Example: `build_execution_intent()`

```python
def build_execution_intent(decision: DecisionPacket, risk: RiskSnapshot, entry_price: float) -> ExecutionIntent:
    if decision.permission != "approve":
        raise ValueError("Execution intent may only be built for approved decisions")

    size = min(0.10, risk.max_position_size)
    return ExecutionIntent(
        decision_id=decision.decision_id,
        broker_path="paper_sim",
        order_type="limit",
        size=size,
        stop_loss=entry_price - 10.0,
        take_profit=entry_price + 20.0,
        time_in_force="DAY",
    )
```

### Example: `journal_trade()`

```python
def journal_trade(setup: CandidateSetup, decision: DecisionPacket, entry: float, exit: float) -> TradeJournalRecord:
    pnl = exit - entry
    outcome = "win" if pnl > 0 else "loss" if pnl < 0 else "scratch"
    return TradeJournalRecord(
        trade_id=f"trade_{uuid4().hex[:12]}",
        setup_id=setup.setup_id,
        decision_id=decision.decision_id,
        entry=entry,
        exit=exit,
        mae=-3.0,
        mfe=12.0,
        outcome=outcome,
        post_trade_notes="Paper-trade replay completed successfully",
    )
```

### Example: End-to-End Paper Slice

```python
def run_oracle_layer_one() -> dict:
    setup = ingest_candidate_setup("NQ", ["msb_up", "ema_alignment", "opening_range_break"])
    setup = enrich_market_context(setup, "ny_open", "above_pdh", "breakout")
    truth = validate_truth(setup)
    decision = decide_permission(setup, truth)

    if decision.permission != "approve":
        return {
            "setup": setup.model_dump(),
            "truth": truth.model_dump(),
            "decision": decision.model_dump(),
            "status": "blocked_before_execution",
        }

    risk = freeze_risk_snapshot(setup.instrument)
    execution = build_execution_intent(decision, risk, entry_price=18250.0)
    journal = journal_trade(setup, decision, entry=18250.0, exit=18268.0)

    return {
        "setup": setup.model_dump(),
        "truth": truth.model_dump(),
        "decision": decision.model_dump(),
        "risk": risk.model_dump(),
        "execution": execution.model_dump(),
        "journal": journal.model_dump(),
    }
```

This is the smallest layer that makes ORACLE real in practice: **signal in, context added, truth checked, decision made, risk frozen, paper execution planned, and result journaled**.

## P2: Replay and Drift Tooling

The repository already emphasizes memory, journaling, promotion/retirement logic, and iterative learning.[1] [2] The additive implementation step is to make those processes inspectable.

| Tooling Surface | Minimum Deliverable |
|---|---|
| **Decision Replay Viewer** | Show every domain contribution for a past setup |
| **Risk Veto Ledger** | Show why trades were blocked or resized |
| **Genome Performance Dashboard** | Show results by state, session, and instrument |
| **Drift Monitor** | Flag when live behavior diverges from validated expectations |
| **Post-Mortem Template** | Structured review for failed executions or false approvals |

## Probabilistic and State-Based Maturity

The current repository already treats market conditions as stateful and context-dependent.[1] [2] A useful additive next step is to make the probabilistic layer explicit rather than implicit.

| Additive Capability | Example Benefit |
|---|---|
| **State transition matrix** | Estimate how often compression leads to expansion or failure |
| **Confidence decomposition** | Separate signal confidence from truth confidence and execution confidence |
| **Regime-conditioned scoring** | Prevent one strategy from being treated as universal |
| **Outcome priors by session and state** | Tie deployment permissions to empirical evidence |

This does not contradict the current architecture. It operationalizes it.

## Execution Discipline

ORACLE’s architecture already separates decision, risk, and execution conceptually.[1] [2] The additive rule for implementation should be:

> No execution component may derive its own trading thesis. It may only act on a validated **Execution Intent** that has already survived Truth, Decision, and Risk governance.

That one implementation rule will prevent much of the coupling risk that typically destroys trading systems.

## Recommended File Additions After This Note

The safest next additive artifacts would be code-adjacent schema definitions, example payloads, and replay fixtures. A `schemas/` directory for the core trading models, an `examples/` directory for end-to-end candidate-setup payloads, and a `replay/` directory for simulated trade traces would convert the blueprint into something testable without disturbing existing documentation.[1] [2]

## TL;DR

LEVIATHAN AI does not need a conceptual rewrite. It needs strict schemas, one replayable vertical slice, visible risk-veto logging, and measurable drift detection. If those are added first, the rest of the architecture can scale with much less structural risk.

## References

[1]: ../README.md "LEVIATHAN AI README"
[2]: ./claude-code-transferable-architecture.md "ORACLE Claude Code Transferable Architecture"
