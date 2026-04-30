# LEVIATHAN AI Paper-Trade Replay Example

**Status:** Additive pre-handoff implementation appendix  
**Purpose:** Show one full replayable ORACLE cycle so CodeSpring can build the first real working path before any live execution

## Why This Document Exists

ORACLE becomes substantially easier to implement once the architecture can be walked end to end using a single representative case.[1] [2] This appendix provides that first full replay example. It is intentionally focused on **paper simulation**, because the first priority is not brokerage access. The first priority is proving that the signal, truth, decision, risk, execution, and journal layers all produce consistent artifacts.[1] [2] [3] [4]

## Scenario Summary

The following replay simulates a Nasdaq futures opening-range breakout that survives truth validation, passes risk review, and completes as a paper-trade win.

| Stage | Result |
|---|---|
| Signal ingress | A valid bullish candidate setup enters the system |
| State enrichment | The setup is labeled as `ny_open` and `breakout` |
| Truth validation | External truth layers confirm buy-side pressure |
| Decision | ORACLE approves a long breakout-retest structure |
| Risk | The trade remains within current risk limits |
| Execution | A paper-simulation intent is created |
| Journal | The replay is stored as a completed trade record |

## End-to-End Replay Objects

### 1. Candidate Setup

```json
{
  "setup_id": "setup_replay_001",
  "instrument": "NQ",
  "timestamp": "2026-04-15T14:35:00Z",
  "signal_features": [
    "opening_range_break",
    "msb_up",
    "ema_alignment",
    "liquidity_sweep_complete"
  ],
  "session_label": "ny_open",
  "range_label": "above_opening_range_high",
  "state_label": "breakout",
  "liquidity_features": ["equal_highs_swept", "fair_value_gap_below"]
}
```

### 2. Truth Validation

```json
{
  "setup_id": "setup_replay_001",
  "orderbook_bias": "bullish",
  "options_context": "No bearish block flow contradiction present.",
  "event_risk": "safe",
  "sentiment_modifier": 0.05,
  "truth_status": "confirmed",
  "notes": "Buyers accepted price above the opening range after the sweep and held the retest."
}
```

### 3. Decision Packet

```json
{
  "decision_id": "dec_replay_001",
  "setup_id": "setup_replay_001",
  "permission": "approve",
  "direction": "long",
  "confidence": 0.74,
  "entry_style": "breakout_retest",
  "scaling_allowed": true,
  "justification": "Signal, state, liquidity, and truth layers are aligned."
}
```

### 4. Risk Snapshot

```json
{
  "session_id": "session_replay_001",
  "max_daily_drawdown": 1.5,
  "max_position_size": 0.25,
  "allowed_instruments": ["NQ"],
  "prop_firm_rules": ["daily_dd_lock", "loss_streak_throttle", "no_overnight_hold"],
  "frozen_at": "2026-04-15T14:35:01Z"
}
```

### 5. Execution Intent

```json
{
  "decision_id": "dec_replay_001",
  "broker_path": "paper_sim",
  "order_type": "limit",
  "size": 0.1,
  "stop_loss": 18240.0,
  "take_profit": 18270.0,
  "time_in_force": "DAY"
}
```

### 6. Trade Journal Record

```json
{
  "trade_id": "trade_replay_001",
  "setup_id": "setup_replay_001",
  "decision_id": "dec_replay_001",
  "entry": 18250.0,
  "exit": 18268.0,
  "mae": -3.0,
  "mfe": 18.0,
  "outcome": "win",
  "post_trade_notes": "Replay confirms that the paper path can preserve the same object lineage from setup through journal."
}
```

## Example Replay Pipeline Functions

```python
from typing import Any


def replay_candidate_setup() -> dict[str, Any]:
    return {
        "setup_id": "setup_replay_001",
        "instrument": "NQ",
        "timestamp": "2026-04-15T14:35:00Z",
        "signal_features": ["opening_range_break", "msb_up", "ema_alignment", "liquidity_sweep_complete"],
        "session_label": "ny_open",
        "range_label": "above_opening_range_high",
        "state_label": "breakout",
        "liquidity_features": ["equal_highs_swept", "fair_value_gap_below"],
    }


def replay_truth_validation(setup: dict[str, Any]) -> dict[str, Any]:
    return {
        "setup_id": setup["setup_id"],
        "orderbook_bias": "bullish",
        "options_context": "No bearish block flow contradiction present.",
        "event_risk": "safe",
        "sentiment_modifier": 0.05,
        "truth_status": "confirmed",
        "notes": "Buyers accepted price above the opening range after the sweep and held the retest.",
    }


def replay_decision(setup: dict[str, Any], truth: dict[str, Any]) -> dict[str, Any]:
    permission = "approve" if truth["truth_status"] == "confirmed" else "wait"
    return {
        "decision_id": "dec_replay_001",
        "setup_id": setup["setup_id"],
        "permission": permission,
        "direction": "long",
        "confidence": 0.74,
        "entry_style": "breakout_retest",
        "scaling_allowed": True,
        "justification": "Signal, state, liquidity, and truth layers are aligned.",
    }


def replay_risk() -> dict[str, Any]:
    return {
        "session_id": "session_replay_001",
        "max_daily_drawdown": 1.5,
        "max_position_size": 0.25,
        "allowed_instruments": ["NQ"],
        "prop_firm_rules": ["daily_dd_lock", "loss_streak_throttle", "no_overnight_hold"],
        "frozen_at": "2026-04-15T14:35:01Z",
    }


def replay_execution(decision: dict[str, Any], risk: dict[str, Any]) -> dict[str, Any]:
    if decision["permission"] != "approve":
        raise ValueError("Replay cannot build execution for a non-approved trade")
    return {
        "decision_id": decision["decision_id"],
        "broker_path": "paper_sim",
        "order_type": "limit",
        "size": min(0.10, risk["max_position_size"]),
        "stop_loss": 18240.0,
        "take_profit": 18270.0,
        "time_in_force": "DAY",
    }


def replay_journal(setup: dict[str, Any], decision: dict[str, Any]) -> dict[str, Any]:
    return {
        "trade_id": "trade_replay_001",
        "setup_id": setup["setup_id"],
        "decision_id": decision["decision_id"],
        "entry": 18250.0,
        "exit": 18268.0,
        "mae": -3.0,
        "mfe": 18.0,
        "outcome": "win",
        "post_trade_notes": "Replay confirms a consistent object lineage from ingress to journal.",
    }
```

## Example Full Replay Runner

```python
def run_oracle_paper_replay() -> dict[str, Any]:
    setup = replay_candidate_setup()
    truth = replay_truth_validation(setup)
    decision = replay_decision(setup, truth)
    risk = replay_risk()
    execution = replay_execution(decision, risk)
    journal = replay_journal(setup, decision)

    return {
        "setup": setup,
        "truth": truth,
        "decision": decision,
        "risk": risk,
        "execution": execution,
        "journal": journal,
    }
```

## What CodeSpring Should Prove First

| Validation Goal | Meaning |
|---|---|
| **Object continuity** | The same `setup_id` and `decision_id` flow through the whole replay |
| **Risk discipline** | No execution object appears without decision and risk approval |
| **Journal completeness** | The pipeline always ends with a trade record or a blocked-trade record |
| **Replay determinism** | The same replay fixture should produce the same result each time |

## TL;DR

Before ORACLE touches live capital, CodeSpring should make this replay path work cleanly, deterministically, and transparently. If that is stable, the rest of the trading architecture becomes much safer to extend.[1] [2]

## References

[1]: ../README.md "LEVIATHAN AI README"
[2]: ./claude-code-transferable-architecture.md "ORACLE Claude Code Transferable Architecture"
[3]: ./oracle-schema-contracts-and-example-payloads.md "LEVIATHAN AI Schema Contracts and Example Payloads"
[4]: ./additive-implementation-priorities.md "LEVIATHAN AI Additive Implementation Priorities"
