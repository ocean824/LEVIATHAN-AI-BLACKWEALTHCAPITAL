# LEVIATHAN AI ↔ ØMEGA AI Integration Alignment Note

**Status:** Additive integration clarification  
**Scope:** Non-destructive alignment of LEVIATHAN’s integration model with the canonical ØMEGA control-plane naming

## Purpose

This note aligns LEVIATHAN AI’s external integration language with the clarified ØMEGA control-plane convention established in the companion ØMEGA documentation. It does **not** modify or invalidate any existing LEVIATHAN or ØMEGA architecture document. It simply provides a stable interpretation rule for future implementation work.[1] [2] [3]

The core clarification is that **ØMEGA AI** remains the name of the full multi-agent system, while **PRIME** is the canonical name of the top-level controlling agent within that system. Therefore, when LEVIATHAN integrates upward into the broader platform, its primary top-level orchestration counterpart should be treated as **PRIME**. If historical documents use **DOMINION** for that same role, future implementation should map that reference to **PRIME** unless explicitly separated later.[2] [3]

## Integration Boundary

LEVIATHAN AI should remain a **specialized trading organism**, not a generic controller. PRIME should remain the **cross-domain command authority** inside ØMEGA AI. That distinction is important because it preserves LEVIATHAN’s trading rigor while preventing orchestration concerns from leaking into the trading core.[1] [2]

| Component | Canonical Role | Primary Responsibility |
|---|---|---|
| **ØMEGA AI** | Overall multi-agent operating system | Cross-domain ecosystem containing all agents and subsystems |
| **PRIME** | Top-level controlling agent | Routing, approval policy, escalation, cross-agent coordination |
| **LEVIATHAN AI** | Specialized trading intelligence system | Market interpretation, trade permission logic, risk-aware execution planning |
| **QUANTUM** | ØMEGA-side trading interface agent | The point through which PRIME interacts with LEVIATHAN inside the broader agent hierarchy |
| **ORCA AI** | LEVIATHAN internal market-intelligence sub-agent | Handles signal interpretation, market-state enrichment, liquidity context, and truth-layer synthesis |
| **MEGALODON AI** | LEVIATHAN internal execution sub-agent | Handles execution orchestration, position-management enforcement, and high-conviction deployment flow |

## Recommended Handshake Model

The cleanest additive integration model is a bounded handshake between PRIME and LEVIATHAN, typically mediated through QUANTUM when operating inside the ØMEGA hierarchy. Inside LEVIATHAN itself, ORCA AI can own the market-intelligence side of the response while MEGALODON AI owns the execution-facing side once a trade has cleared decision and risk governance.[1] [2]

| Handshake Type | Source | Destination | Purpose |
|---|---|---|---|
| **Status Heartbeat** | LEVIATHAN / QUANTUM | PRIME | Broadcast current market bias, risk state, and operating mode |
| **Inquiry / Response** | PRIME | LEVIATHAN / QUANTUM | Request current trade thesis, state classification, or deployment readiness |
| **Kill-Switch Sync** | PRIME or LEVIATHAN | Counterparty | Ensure emergency halt propagates across both control planes |
| **Restriction Broadcast** | PRIME | LEVIATHAN | Apply global business or security restrictions without modifying trading logic |
| **Execution Summary** | LEVIATHAN | PRIME | Report completed, blocked, or vetoed trade cycles for cross-system awareness |

## Minimal Shared Contract

The integration should rely on explicit payloads rather than informal prompt descriptions.

| Payload | Minimum Fields |
|---|---|
| **LeviathanHeartbeat** | `timestamp`, `operating_mode`, `market_bias`, `risk_state`, `active_restrictions`, `confidence_band` |
| **LeviathanInquiry** | `request_id`, `requested_by`, `goal`, `instrument_scope`, `urgency`, `approval_mode` |
| **LeviathanDecisionSummary** | `request_id`, `permission`, `direction`, `confidence`, `risk_status`, `reason_code` |
| **KillSwitchEvent** | `event_id`, `trigger_source`, `severity`, `scope`, `effective_until`, `notes` |

## First-Layer Handshake Code Examples

The first real integration layer should be small enough to test in isolation. It should prove that PRIME can request bounded trading context from LEVIATHAN, LEVIATHAN can answer with a typed summary, and both sides can synchronize a safety stop.

| Function | Responsibility |
|---|---|
| `build_leviathan_heartbeat()` | Publish LEVIATHAN runtime state to PRIME |
| `build_leviathan_inquiry()` | Let PRIME request bounded trading intelligence |
| `respond_with_decision_summary()` | Return a typed LEVIATHAN response |
| `sync_kill_switch()` | Propagate emergency halt semantics across systems |

### Example: Shared Integration Models

```python
from datetime import datetime, UTC
from typing import Literal
from uuid import uuid4
from pydantic import BaseModel, Field


class LeviathanHeartbeat(BaseModel):
    timestamp: str
    operating_mode: Literal["research", "advisory", "semi_auto", "full_auto", "signal_only"]
    market_bias: Literal["bullish", "bearish", "neutral"]
    risk_state: Literal["normal", "reduced", "halted"]
    active_restrictions: list[str] = Field(default_factory=list)
    confidence_band: float


class LeviathanInquiry(BaseModel):
    request_id: str
    requested_by: str
    goal: str
    instrument_scope: list[str]
    urgency: Literal["low", "normal", "high", "critical"]
    approval_mode: Literal["autonomous", "confirmation_required", "blocked"]


class LeviathanDecisionSummary(BaseModel):
    request_id: str
    permission: Literal["reject", "wait", "approve", "signal_only"]
    direction: Literal["long", "short", "flat"]
    confidence: float
    risk_status: Literal["clear", "restricted", "halted"]
    reason_code: str


class KillSwitchEvent(BaseModel):
    event_id: str
    trigger_source: str
    severity: Literal["high", "critical"]
    scope: Literal["oracle_only", "omega_only", "global"]
    effective_until: str
    notes: str
```

### Example: `build_leviathan_heartbeat()`

```python
def build_leviathan_heartbeat() -> LeviathanHeartbeat:
    return LeviathanHeartbeat(
        timestamp=datetime.now(UTC).isoformat(),
        operating_mode="semi_auto",
        market_bias="bullish",
        risk_state="normal",
        active_restrictions=["macro_event_watch"],
        confidence_band=0.71,
    )
```

### Example: `build_leviathan_inquiry()`

```python
def build_leviathan_inquiry(goal: str, instruments: list[str]) -> LeviathanInquiry:
    return LeviathanInquiry(
        request_id=f"inq_{uuid4().hex[:12]}",
        requested_by="PRIME",
        goal=goal,
        instrument_scope=instruments,
        urgency="high",
        approval_mode="confirmation_required",
    )
```

### Example: `respond_with_decision_summary()`

```python
def respond_with_decision_summary(inquiry: LeviathanInquiry, heartbeat: LeviathanHeartbeat) -> LeviathanDecisionSummary:
    if heartbeat.risk_state == "halted":
        return LeviathanDecisionSummary(
            request_id=inquiry.request_id,
            permission="reject",
            direction="flat",
            confidence=0.0,
            risk_status="halted",
            reason_code="oracle_halted",
        )

    return LeviathanDecisionSummary(
        request_id=inquiry.request_id,
        permission="signal_only",
        direction="long" if heartbeat.market_bias == "bullish" else "flat",
        confidence=heartbeat.confidence_band,
        risk_status="clear",
        reason_code="context_ready_manual_confirmation_required",
    )
```

### Example: `sync_kill_switch()`

```python
def sync_kill_switch(trigger_source: str, scope: str, notes: str) -> KillSwitchEvent:
    return KillSwitchEvent(
        event_id=f"halt_{uuid4().hex[:12]}",
        trigger_source=trigger_source,
        severity="critical",
        scope=scope,
        effective_until=datetime.now(UTC).isoformat(),
        notes=notes,
    )
```

### Example: Minimal PRIME ↔ LEVIATHAN Round Trip

```python
def run_prime_leviathan_handshake() -> dict:
    heartbeat = build_leviathan_heartbeat()
    inquiry = build_leviathan_inquiry(
        goal="Assess whether NQ conditions justify signal-only monitoring",
        instruments=["NQ"],
    )
    decision = respond_with_decision_summary(inquiry, heartbeat)

    return {
        "heartbeat": heartbeat.model_dump(),
        "inquiry": inquiry.model_dump(),
        "decision": decision.model_dump(),
    }
```

This is enough to prove the first real integration layer: **PRIME asks, LEVIATHAN answers, both sides speak typed contracts, and safety synchronization remains available**.

## Authority Rule

The integration should follow a simple non-conflicting authority rule.

> **PRIME may coordinate, request, restrict, and halt. LEVIATHAN may decide, veto, or decline within the trading domain according to its own sovereign risk and truth logic.**

This keeps LEVIATHAN from becoming a mere order runner while also ensuring the larger platform can impose global safety controls.

## What Should Not Happen

A structurally weak integration would let PRIME bypass LEVIATHAN’s decision and risk layers to force execution, or let LEVIATHAN silently ignore system-wide restrictions. The safer additive principle is that both systems communicate through explicit contracts, clear veto semantics, and auditable state transitions.[1] [2]

## Recommended Next Additions

The most useful next additive artifacts would be example JSON payloads for the shared handshake types, a sequence diagram for PRIME → QUANTUM → LEVIATHAN interaction, and a short policy matrix defining which restrictions are advisory versus mandatory.

## References

[[1]: ../README.md "LEVIATHAN AI README"
[2]: ./claude-code-transferable-architecture.md "LEVIATHAN Claude Code Transferable Architecture"e"
[3]: ../../XYRASYSTEMS---OMEGA-AI/docs/canonical-control-plane-addendum.md "ØMEGA AI Canonical Control-Plane Addendum"
