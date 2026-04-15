# ORACLE AI Implementation Module Map

**Status:** Additive pre-handoff implementation appendix  
**Purpose:** Translate the ORACLE AI documentation into a concrete codebase layout and service decomposition for CodeSpring

## Why This Document Exists

ORACLE’s repo already contains enough architecture to justify a serious implementation effort.[1] [2] What CodeSpring still benefits from is a tighter mapping from documentation to code structure. This appendix provides that map so the handoff is not just conceptual, but operational.[1] [2] [3]

## Guiding Principle

The codebase should mirror the system’s logical separation. Research should not be embedded inside execution. Risk should not be hidden inside broker adapters. Replay should not be an afterthought. A clean layout makes those boundaries harder to violate.

## Suggested Repository Structure

| Path | Purpose |
|---|---|
| `src/oracle/schemas/` | Shared typed contracts for setup, truth, decision, risk, execution, and journal layers |
| `src/oracle/research/` | Strategy genome storage, research ingestion, validation history |
| `src/oracle/ingress/` | TradingView bot signals, webhook receivers, raw event intake |
| `src/oracle/state/` | Session, range, state labeling, and transition logic |
| `src/oracle/truth/` | Order-flow checks, event filters, external truth connectors |
| `src/oracle/decision/` | Decision synthesis and permission logic |
| `src/oracle/risk/` | Sovereign risk engine and veto rules |
| `src/oracle/execution/` | Paper simulator, MT5 bridge, direct broker adapters |
| `src/oracle/journal/` | Trade logging, replay, and post-trade analysis |
| `src/oracle/integration/` | ØMEGA / PRIME / QUANTUM integration contracts |
| `src/oracle/tests/` | Replay fixtures, schema validation, integration tests |

## Example Directory Tree

```text
src/
  oracle/
    schemas/
      strategy.py
      setup.py
      truth.py
      decision.py
      risk.py
      execution.py
      journal.py
      integration.py
    research/
      genome_store.py
      validation_registry.py
    ingress/
      tradingview_webhook.py
      signal_router.py
    state/
      session_classifier.py
      range_classifier.py
      transition_engine.py
    truth/
      orderflow_validator.py
      event_risk_filter.py
      sentiment_adapter.py
    decision/
      decision_engine.py
      confidence_model.py
    risk/
      veto_engine.py
      prop_firm_rules.py
    execution/
      paper_sim.py
      mt5_bridge.py
      broker_router.py
    journal/
      trade_journal.py
      replay_loader.py
      drift_monitor.py
    integration/
      prime_handshake.py
      heartbeat_router.py
    tests/
      fixtures/
        replay_nq_breakout.json
      test_schema_contracts.py
      test_paper_replay.py
```

## Module-to-Document Mapping

| Existing Document | Target Code Area |
|---|---|
| `README.md` | Overall service boundaries and build order |
| `CODESPRING-MASTER-INSTRUCTIONS.md` | High-level implementation sequence |
| `docs/claude-code-transferable-architecture.md` | Shared architectural patterns and feedback loops |
| `docs/oracle-schema-contracts-and-example-payloads.md` | `src/oracle/schemas/` |
| `docs/market-state-transition-matrix.md` | `src/oracle/state/transition_engine.py` |
| `docs/risk-veto-policy-matrix.md` | `src/oracle/risk/veto_engine.py` |
| `docs/paper-trade-replay-example.md` | `src/oracle/tests/fixtures/` and `src/oracle/execution/paper_sim.py` |
| `docs/omega-prime-integration-alignment.md` | `src/oracle/integration/` |

## Example Skeleton Interfaces

```python
class DecisionEngine:
    def evaluate(self, setup, truth, state_context):
        raise NotImplementedError


class RiskVetoEngine:
    def assess(self, decision, account_state, market_context):
        raise NotImplementedError


class PaperExecutionEngine:
    def simulate(self, execution_intent):
        raise NotImplementedError
```

## Recommended Build Order

| Build Step | Target Module | Why First |
|---|---|---|
| 1 | `schemas/` | Shared contracts reduce ambiguity everywhere else |
| 2 | `tests/fixtures/` | Replay examples make the build testable immediately |
| 3 | `state/` + `truth/` | These shape decision quality |
| 4 | `decision/` + `risk/` | These define whether a trade may exist |
| 5 | `execution/paper_sim.py` | Lets the system work without live capital |
| 6 | `journal/` | Makes review and drift detection real |
| 7 | `integration/` | Connects ORACLE cleanly into ØMEGA |
| 8 | Live adapters | Only after the paper path is proven |

## Handoff Standard

The minimum acceptable CodeSpring handoff should result in a codebase where the following statement is true:

> A single replay fixture can enter through ingress, be classified by state, validated by truth, approved or blocked by decision and risk, simulated by paper execution, and recorded by the journal layer.

If that statement is true, ORACLE has a real spine. If it is not true, the build is still mostly conceptual.

## TL;DR

This module map helps CodeSpring build ORACLE as a layered organism rather than a pile of trading features. It protects the architecture by giving each concept a clean home.[1] [2] [3]

## References

[1]: ../README.md "ORACLE AI README"
[2]: ./claude-code-transferable-architecture.md "ORACLE Claude Code Transferable Architecture"
[3]: ./paper-trade-replay-example.md "ORACLE AI Paper-Trade Replay Example"
