# LEVIATHAN AI Risk-Veto Policy Matrix

**Status:** Additive pre-handoff implementation appendix  
**Purpose:** Define when the Sovereign Risk Engine may reduce, block, or halt decisions produced by the trading logic

## Why This Document Exists

ORACLE’s architecture is strongest when the system’s layers remain separate: research defines the doctrine, signal and truth define the opportunity, decision defines the trade thesis, and risk defines the non-negotiable guardrails.[1] [2] If the risk layer is vague, the execution path becomes vulnerable to improvisation. This document makes the veto semantics explicit so CodeSpring can build the system without ambiguity.[1] [2] [3]

## Governance Principle

> **The Risk Engine does not create trade ideas. It governs whether a proposed trade may proceed, must shrink, must wait, or must stop.**

That separation keeps ORACLE from becoming structurally self-contradictory.

## Core Veto Categories

| Category | Description | Typical Result |
|---|---|---|
| **capital_preservation** | Daily or session drawdown protection | Block or halt |
| **rule_compliance** | Prop-firm or platform restrictions | Reject or reshape |
| **exposure_control** | Concentration, correlation, or over-sizing | Reduce size or reject |
| **event_risk** | Macro or calendar uncertainty | Wait or block |
| **market_integrity** | Feed instability, latency, or data disagreement | Block |
| **behavioral_degradation** | Loss streaks, revenge behavior proxies, overtrading | Reduce autonomy or halt |

## Veto Matrix

| Trigger | Severity | Risk Action | Execution Consequence |
|---|---|---|---|
| Daily drawdown threshold breached | Critical | `halt_all_trading` | No new execution intents |
| Three consecutive losses in one session | High | `reduce_size` | Cut maximum size and require stronger confirmation |
| Instrument not allowed under current mandate | High | `reject_instrument` | Decision cannot proceed |
| Major macro event within lockout window | High | `event_lock` | No autonomous approvals |
| Data feed disagreement across truth sources | High | `truth_conflict_hold` | Wait for reconciliation |
| Position size exceeds allowed maximum | Medium | `resize_or_reject` | Reduce size or reject if resizing is invalid |
| Correlated exposure already elevated | Medium | `exposure_throttle` | Cap additional entries |
| Overnight hold not permitted | High | `force_flat_by_session_end` | Auto-close or refuse carry |

## Example Risk Decision Model

```python
from typing import Literal
from pydantic import BaseModel

RiskAction = Literal[
    "allow",
    "reduce_size",
    "wait",
    "reject",
    "halt_all_trading",
    "force_flat_by_session_end",
]


class RiskVetoDecision(BaseModel):
    allowed: bool
    risk_action: RiskAction
    severity: Literal["low", "medium", "high", "critical"]
    reason: str
    adjusted_size: float | None = None
```

## Example Policy Evaluator

```python
def evaluate_risk_veto(
    daily_drawdown: float,
    max_daily_drawdown: float,
    consecutive_losses: int,
    requested_size: float,
    max_position_size: float,
    macro_lockout_active: bool,
) -> RiskVetoDecision:
    if daily_drawdown >= max_daily_drawdown:
        return RiskVetoDecision(
            allowed=False,
            risk_action="halt_all_trading",
            severity="critical",
            reason="Daily drawdown threshold breached",
        )

    if macro_lockout_active:
        return RiskVetoDecision(
            allowed=False,
            risk_action="wait",
            severity="high",
            reason="Major macro event lockout active",
        )

    if consecutive_losses >= 3:
        return RiskVetoDecision(
            allowed=True,
            risk_action="reduce_size",
            severity="high",
            reason="Loss-streak throttle engaged",
            adjusted_size=min(requested_size, max_position_size * 0.5),
        )

    if requested_size > max_position_size:
        return RiskVetoDecision(
            allowed=True,
            risk_action="reduce_size",
            severity="medium",
            reason="Requested size exceeds current risk cap",
            adjusted_size=max_position_size,
        )

    return RiskVetoDecision(
        allowed=True,
        risk_action="allow",
        severity="low",
        reason="No active veto condition",
        adjusted_size=requested_size,
    )
```

## Example Application to an Execution Intent

```python
def apply_risk_veto_to_size(execution_size: float, veto: RiskVetoDecision) -> float:
    if not veto.allowed:
        raise ValueError(f"Execution blocked: {veto.reason}")
    return veto.adjusted_size if veto.adjusted_size is not None else execution_size
```

## Recommended Operating Rules

| Rule | Why It Matters |
|---|---|
| **Risk must evaluate after Decision but before ExecutionIntent is finalized** | Keeps logic orderly and replayable |
| **Every veto should be journaled even if no trade occurs** | Hidden blocked trades still teach the system |
| **Critical risk actions should propagate to ØMEGA / PRIME awareness** | Cross-system safety should not depend on silence |
| **Risk may reduce size without rewriting trade logic** | Preserves role boundaries |
| **Repeated veto patterns should feed the research loop** | Prevents the same invalid setup from returning forever |

## TL;DR

ORACLE becomes much safer to build when the risk layer is not just a concept but a **typed veto authority** with explicit consequences. This matrix gives CodeSpring that authority surface.[1] [2]

## References

[1]: ../README.md "LEVIATHAN AI README"
[2]: ./claude-code-transferable-architecture.md "ORACLE Claude Code Transferable Architecture"
[3]: ./additive-implementation-priorities.md "LEVIATHAN AI Additive Implementation Priorities"
