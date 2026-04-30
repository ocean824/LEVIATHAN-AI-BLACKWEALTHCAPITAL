# LEVIATHAN AI Market-State Transition Matrix

**Status:** Additive pre-handoff implementation appendix  
**Purpose:** Make ORACLE’s market-regime logic explicit enough to drive replay, filtering, and deployment decisions

## Why This Document Exists

ORACLE’s architecture already assumes that market behavior is stateful rather than uniform.[1] [2] What still helps before implementation is a more explicit transition grammar: what the current state means, what transitions are normal, what transitions are suspicious, and how the system should react when state changes under an active setup.[1] [2] [3]

This document provides a first working state matrix for CodeSpring. It is intentionally narrow enough to implement in replay and paper-trading mode.

## Canonical First-Pass Market States

| State | Meaning | Typical Characteristics |
|---|---|---|
| **compression** | Price is storing energy with narrowing expansion | Range tightening, declining follow-through, frequent mean reversion |
| **breakout** | Price has left a prior balance area with directional intent | Structure break, acceptance beyond range edge, stronger momentum |
| **trend_continuation** | Price is continuing in an already established directional auction | Pullbacks are shallow, directional liquidity persists |
| **expansion** | Volatility and range are broadening rapidly | Wide candles, stronger displacement, higher opportunity and higher failure cost |
| **distribution** | Prior up-move is rotating into sell-side transfer | Failed continuation, supply absorption, weaker upside acceptance |
| **accumulation** | Prior down-move is rotating into buy-side transfer | Repeated support defense, failed breakdowns, absorption near lows |
| **mean_reversion** | Directional attempts fail and price rotates back toward a central value | Repeated rejection of extremes, short-lived breakouts |
| **event_locked** | Macro, news, or scheduled event dominates normal market behavior | Elevated randomness, liquidity discontinuity, suppressed deployment |

## Preferred Transition Matrix

| From State | To State | Typical Validity | Recommended Interpretation |
|---|---|---|---|
| compression | breakout | High | Normal release of stored energy |
| breakout | trend_continuation | High | Healthy directional follow-through |
| breakout | mean_reversion | Medium | Failed breakout or incomplete acceptance |
| trend_continuation | expansion | High | Momentum is broadening |
| trend_continuation | distribution | Medium | Direction is tiring and inventory transfer is starting |
| trend_continuation | mean_reversion | Medium | Trend failure or exhaustion |
| distribution | mean_reversion | High | Typical post-distribution rotation |
| accumulation | breakout | High | Strong bullish transition |
| any_state | event_locked | High around scheduled macro events | Reduce or disable autonomous deployment |
| event_locked | compression | Medium | Post-event digestion, wait for clarity |

## Transition Risk Semantics

| Transition Class | Meaning | Suggested Response |
|---|---|---|
| **stable** | State change matches expected auction logic | Allow normal evaluation |
| **caution** | State change is plausible but requires confirmation | Reduce size or require stronger Truth alignment |
| **unstable** | State change suggests incoherence or event distortion | Pause new deployment and wait |

## Example Rule Table

| Transition | Risk Class | Policy Action |
|---|---|---|
| compression → breakout | stable | Evaluate normally |
| breakout → trend_continuation | stable | Evaluate normally |
| breakout → mean_reversion | caution | Require retest confirmation |
| trend_continuation → mean_reversion | caution | Reduce size and confidence |
| any → event_locked | unstable | No autonomous trade approval |
| event_locked → expansion | unstable | Wait for post-event normalization |

## Example State Models

```python
from typing import Literal
from pydantic import BaseModel

MarketState = Literal[
    "compression",
    "breakout",
    "trend_continuation",
    "expansion",
    "distribution",
    "accumulation",
    "mean_reversion",
    "event_locked",
]

TransitionRisk = Literal["stable", "caution", "unstable"]


class StateTransition(BaseModel):
    from_state: MarketState
    to_state: MarketState
    risk_class: TransitionRisk
    policy_action: str
```

## Example Transition Logic

```python
TRANSITION_RULES: dict[tuple[str, str], tuple[str, str]] = {
    ("compression", "breakout"): ("stable", "evaluate_normally"),
    ("breakout", "trend_continuation"): ("stable", "evaluate_normally"),
    ("breakout", "mean_reversion"): ("caution", "require_retest_confirmation"),
    ("trend_continuation", "mean_reversion"): ("caution", "reduce_size_and_confidence"),
    ("event_locked", "expansion"): ("unstable", "wait_for_post_event_normalization"),
}


def classify_state_transition(from_state: str, to_state: str) -> StateTransition:
    risk_class, policy_action = TRANSITION_RULES.get(
        (from_state, to_state),
        ("unstable", "manual_review_required"),
    )
    return StateTransition(
        from_state=from_state,
        to_state=to_state,
        risk_class=risk_class,
        policy_action=policy_action,
    )
```

## Example Use Inside ORACLE

```python
def adjust_decision_confidence(base_confidence: float, transition: StateTransition) -> float:
    if transition.risk_class == "stable":
        return base_confidence
    if transition.risk_class == "caution":
        return max(0.0, base_confidence - 0.15)
    return max(0.0, base_confidence - 0.35)
```

## Practical Build Guidance

CodeSpring does not need to treat this matrix as a final market ontology. It should treat it as the **first version of a replayable regime grammar**. Once the replay framework exists, these transitions can be statistically refined rather than merely debated.

## TL;DR

ORACLE should not reason about “the market” as one thing. It should reason about **state**, **transition**, and **policy response**. This matrix makes that operational.[1] [2]

## References

[1]: ../README.md "LEVIATHAN AI README"
[2]: ./claude-code-transferable-architecture.md "ORACLE Claude Code Transferable Architecture"
[3]: ./additive-implementation-priorities.md "LEVIATHAN AI Additive Implementation Priorities"
