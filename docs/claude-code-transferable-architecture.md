# Transferable Architecture from Claude Code Source to ORACLE AI

> **Source**: [claude-code-from-source.com](https://claude-code-from-source.com/) — 18 chapters reverse-engineering the most sophisticated production AI agent ever built.
> **Purpose**: Apply proven architectural patterns from Claude Code's agent system to ORACLE AI's trading system. These are not theoretical recommendations — they are battle-tested patterns running in production at scale.

---

## Table of Contents

1. [The Async Generator Loop for Market Domains](#1-the-async-generator-loop-for-market-domains)
2. [The 4-Layer Context Compression for Market Memory](#2-the-4-layer-context-compression-for-market-memory)
3. [The Permission Mode System for Risk Governance](#3-the-permission-mode-system-for-risk-governance)
4. [The Tool System for Domain Execution](#4-the-tool-system-for-domain-execution)
5. [The Memory System for Trade Journaling](#5-the-memory-system-for-trade-journaling)
6. [The Hook System for Risk Guardrails](#6-the-hook-system-for-risk-guardrails)
7. [The Sub-Agent Pattern for Domain Specialization](#7-the-sub-agent-pattern-for-domain-specialization)
8. [The Fork Agent Pattern for Parallel Market Analysis](#8-the-fork-agent-pattern-for-parallel-market-analysis)
9. [The Two-Tier State Architecture for Market State](#9-the-two-tier-state-architecture-for-market-state)
10. [The Bootstrap Pipeline for Market Open](#10-the-bootstrap-pipeline-for-market-open)
11. [The Staleness System for Strategy Drift](#11-the-staleness-system-for-strategy-drift)
12. [The Background Extraction Agent for Trade Memory](#12-the-background-extraction-agent-for-trade-memory)
13. [The Snapshot Security Model for Risk Config](#13-the-snapshot-security-model-for-risk-config)
14. [The Stop Hook for Trade Verification](#14-the-stop-hook-for-trade-verification)
15. [Implementation Priority Matrix](#15-implementation-priority-matrix)

---

## 1. The Async Generator Loop for Market Domains

**Claude Code Pattern**: The `query()` function is an async generator (~1,730 lines) that streams model responses, collects tool calls, executes them, appends results, and loops. It yields `Message` objects and returns a discriminated union `Terminal` encoding exactly why the loop stopped (10 terminal states, 7 continuation states).

**ORACLE Application**: The Live Market Flow (14 steps) should be implemented as an async generator, not a sequential pipeline.

```python
class OracleMarketLoop:
    """ORACLE's main market analysis loop — adapted from Claude Code's query.ts."""
    
    async def analyze(self, market_context: MarketContext) -> AsyncGenerator[DomainSignal, None]:
        """Yields DomainSignal objects as each domain completes analysis.
        Returns MarketTerminal with the final decision reason."""
        
        while not self.should_terminate(market_context):
            # 1. Signal Domain generates candidate setup
            signal = await self.signal_domain.evaluate(market_context)
            yield DomainSignal(domain="signal", data=signal)
            
            # 2. Session + Range + State domains enrich context (concurrent)
            enrichments = await asyncio.gather(
                self.session_domain.classify(market_context),
                self.range_domain.classify(market_context),
                self.state_domain.classify(market_context),
                self.liquidity_domain.analyze(market_context),
            )
            for enrichment in enrichments:
                yield DomainSignal(domain=enrichment.source, data=enrichment)
            
            # 3. Truth Domain validates (serial — depends on enrichments)
            truth = await self.truth_domain.validate(market_context, enrichments)
            yield DomainSignal(domain="truth", data=truth)
            
            # 4. Decision Domain synthesizes
            decision = await self.decision_domain.decide(market_context, signal, enrichments, truth)
            yield DomainSignal(domain="decision", data=decision)
            
            # 5. Risk Governance vetoes or permits (SOVEREIGN)
            risk_verdict = await self.risk_domain.evaluate(decision)
            yield DomainSignal(domain="risk", data=risk_verdict)
            
            # 6. Check if context needs compression
            market_context = await self.compress_if_needed(market_context)
        
        return MarketTerminal(reason=self.stop_reason, context=market_context)
    
    # 8 Terminal States for ORACLE
    TERMINAL_STATES = [
        "trade_approved",           # Decision approved, execution begins
        "trade_rejected",           # Decision rejected by any domain
        "risk_veto",                # Risk Governance overrode all other domains
        "session_closed",           # Market session ended
        "prop_firm_halt",           # Prop firm rules triggered halt
        "max_loss_reached",         # Daily drawdown limit hit
        "manual_override",          # User manually stopped
        "system_error",             # Unrecoverable error
    ]
    
    # 5 Continuation States for ORACLE
    CONTINUATION_STATES = [
        "awaiting_confirmation",    # Signal present, waiting for Truth Domain
        "partial_fill",             # Order partially filled, managing remainder
        "scaling_opportunity",      # Existing position, evaluating add
        "state_transition",         # Market state changing, re-evaluating
        "recovery_mode",            # Loss streak, reduced sizing active
    ]
```

**Why this matters**: The generator pattern gives ORACLE natural backpressure (the UI only processes signals as fast as it can render them), clean cancellation (abort a market analysis mid-stream), and typed terminal states (every analysis ends with an explicit reason that can be logged and audited).

---

## 2. The 4-Layer Context Compression for Market Memory

**Claude Code Pattern**: 4-layer compression system (tool result budget → snip compact → microcompact → context collapse → auto-compact) with circuit breakers.

**ORACLE Application**: The Memory Domain accumulates massive amounts of data per session — tick data, order book snapshots, domain signals, trade journals. Without compression, the context window fills within minutes of active trading.

```python
class MarketContextCompressor:
    """4-layer compression for ORACLE's market memory."""
    
    LAYERS = {
        0: "tick_budget",        # Per-tick: keep only OHLCV + key L2 levels, discard raw book
        1: "signal_snip",        # Replace old domain signals with [snipped] markers
        2: "session_compact",    # Compress completed sessions into summary statistics
        3: "history_collapse",   # Collapse entire trading days into P&L + key lessons
        4: "auto_summarize",     # LLM summarizes trading history into strategy insights
    }
    
    # Per-domain output budgets (characters)
    DOMAIN_BUDGETS = {
        "signal": 5_000,         # Current signals only
        "truth": 10_000,         # L2 data is verbose
        "session": 2_000,        # Session labels are compact
        "state": 2_000,          # State machine is compact
        "decision": 3_000,       # Decision rationale
        "risk": 1_000,           # Risk verdicts are binary
    }
    
    # Aggregate budget per analysis cycle
    AGGREGATE_BUDGET = 50_000    # chars
```

**Why this matters**: ORACLE processes continuous market data. Without explicit compression layers, the system either runs out of context or loses critical historical patterns. The circuit breaker (max 3 auto-compact failures) prevents infinite compression loops during volatile markets.

---

## 3. The Permission Mode System for Risk Governance

**Claude Code Pattern**: 7 named permission modes (bypass, dontAsk, auto, acceptEdits, default, plan, bubble) with a resolution chain.

**ORACLE Application**: The Risk Governance Domain (SOVEREIGN) maps directly to this pattern. ORACLE's 7 Operating Modes become permission modes that control what actions the system can take.

| ORACLE Mode | Claude Code Equivalent | What It Controls |
|-------------|----------------------|-----------------|
| **Research** | `plan` (read-only) | Can analyze but cannot place orders. All execution blocked. |
| **Advisory** | `default` (user approves) | Generates recommendations. User must approve each trade. |
| **Semi-Automatic** | `acceptEdits` (auto-approve safe) | Auto-executes within pre-approved parameters. Prompts for exceptions. |
| **Full Automatic** | `dontAsk` (all allowed, logged) | Executes all approved strategies. Everything logged. No prompts. |
| **Prop Firm** | `auto` (LLM classifier) | LLM classifier evaluates each trade against prop firm rules before execution. |
| **Recovery** | Custom (restricted) | Reduced position sizing. Loss-streak throttles active. Some strategies disabled. |
| **Signal-Only** | `plan` + output | Read-only analysis with signal output. No execution capability. |

```python
class OraclePermissionSystem:
    """Risk-as-permission-mode system for ORACLE."""
    
    MODES = {
        "research":       {"can_execute": False, "can_analyze": True,  "can_alert": False},
        "advisory":       {"can_execute": False, "can_analyze": True,  "can_alert": True},
        "semi_automatic": {"can_execute": True,  "requires_approval": True,  "auto_approve_within": "pre_approved_params"},
        "full_automatic": {"can_execute": True,  "requires_approval": False, "logging": "mandatory"},
        "prop_firm":      {"can_execute": True,  "requires_approval": "llm_classifier", "extra_rules": "prop_firm_set"},
        "recovery":       {"can_execute": True,  "max_risk_multiplier": 0.5, "disabled_strategies": "loss_streak_set"},
        "signal_only":    {"can_execute": False, "can_analyze": True,  "can_alert": True, "output_format": "signal"},
    }
    
    # Resolution chain: Trade request → Check mode → If prop_firm, run LLM classifier
    # → If semi_auto, check pre-approved params → If advisory, prompt user → Execute or reject
```

**Why this matters**: Named modes replace scattered `if` checks throughout the codebase. Every domain can ask "what mode are we in?" and get a consistent answer. Mode transitions are explicit and logged.

---

## 4. The Tool System for Domain Execution

**Claude Code Pattern**: Tools carry their own permission logic, concurrency declarations, progress reporting, and UI rendering. The `buildTool()` factory has fail-closed defaults (`isParallelSafe: false`, `isReadOnly: false`).

**ORACLE Application**: Each domain's operations become self-describing tools.

```python
class OracleTool:
    """Self-describing tool for ORACLE domain operations."""
    
    name: str
    domain: str                          # Which domain owns this tool
    is_concurrent_safe: bool = False     # Can run in parallel with other tools?
    is_read_only: bool = False           # Does it only read market data?
    requires_risk_approval: bool = True  # Must pass Risk Governance?
    max_execution_time: int = 30         # seconds
    
    # Input-dependent concurrency (from Claude Code's BashTool pattern)
    def is_concurrency_safe(self, input_data: dict) -> bool:
        """Same tool can be safe or unsafe depending on input."""
        if self.domain == "truth" and input_data.get("source") == "l2_snapshot":
            return True   # Reading L2 data is always safe in parallel
        if self.domain == "execution":
            return False  # Execution is NEVER concurrent
        return self.is_read_only

# Fail-closed defaults for new tools
TOOL_DEFAULTS = {
    "is_concurrent_safe": False,    # New tools run serially
    "is_read_only": False,          # Treated as writes (safe default)
    "requires_risk_approval": True, # Must pass risk check (safe default)
}
```

**Why this matters**: When adding a new data source or execution venue, the developer defines the tool's safety properties once. The orchestrator automatically handles concurrency, permissions, and error recovery without central code changes.

---

## 5. The Memory System for Trade Journaling

**Claude Code Pattern**: File-based memory with 4-type taxonomy (user, feedback, project, reference), YAML frontmatter, LLM-powered recall, staleness warnings, and a derivability test.

**ORACLE Application**: The Memory Domain should adopt the same taxonomy, adapted for trading.

| Claude Code Type | ORACLE Equivalent | What It Captures |
|-----------------|-------------------|-----------------|
| **User** | **Trader Profile** | Risk tolerance, preferred instruments, session preferences, experience level |
| **Feedback** | **Trade Corrections** | "Don't trade breakouts in Asian session" — corrections from losing trades |
| **Project** | **Active Campaigns** | Current positions, pending orders, strategy allocations, prop firm status |
| **Reference** | **Market Bookmarks** | Key levels, earnings dates, FOMC schedule, prop firm rule URLs |

```yaml
# Example ORACLE memory file: feedback_asian_breakouts.md
---
name: Asian Session Breakout Warning
description: Breakouts during Asian session have 73% failure rate on ES futures
type: feedback
---

Do not trade breakout strategies during Asian session (18:00-02:00 ET) on ES/NQ.

**Why:** Backtested 847 Asian session breakout signals from 2024-2025. 
73% failed within 15 minutes. The session lacks follow-through volume.

**How to apply:** When Session Domain returns "asian" AND Signal Domain 
returns "breakout", Decision Domain must downgrade to "signal-only" or "reject".
```

**The Derivability Test**: Do NOT save as memory anything that can be re-derived from market data. Price levels, indicator values, chart patterns — all derivable. What to save: trader corrections, strategy performance insights, prop firm rule interpretations, and institutional knowledge about market behavior.

**Recall Pipeline**: At the start of each analysis cycle, a lightweight LLM side-query selects which memories are relevant to the current market context. A memory about Asian session breakouts is only loaded when the Session Domain reports "asian."

---

## 6. The Hook System for Risk Guardrails

**Claude Code Pattern**: 27+ lifecycle events with 6 hook types. Exit code 2 blocks execution. The Stop hook forces continuation. Snapshot security freezes config at startup.

**ORACLE Application**: The Risk Governance Domain (SOVEREIGN) is implemented as a hook system, not a monolithic function.

```python
class OracleHookSystem:
    """Risk guardrails implemented as lifecycle hooks."""
    
    # ORACLE Lifecycle Events (mapped from Claude Code's 27+)
    EVENTS = {
        # Pre-execution hooks (can BLOCK)
        "PreTradeSubmit":      "Before any order is sent to broker",
        "PrePositionScale":    "Before adding to existing position",
        "PreStrategyActivate": "Before enabling a strategy for live trading",
        
        # Post-execution hooks (observe + inject context)
        "PostFill":            "After order fill confirmed",
        "PostSessionClose":    "After market session ends",
        "PostLoss":            "After a losing trade closes",
        
        # Decision hooks
        "PreDecision":         "Before Decision Domain synthesizes",
        "PostDecision":        "After Decision Domain outputs, before execution",
        
        # System hooks
        "MarketOpen":          "At session open",
        "MarketClose":         "At session close",
        "DailyReset":          "At midnight, reset daily counters",
        "PropFirmCheck":       "Periodic prop firm compliance check",
    }
    
    # Exit code semantics (from Claude Code)
    EXIT_CODES = {
        0: "Pass — trade approved",
        2: "BLOCK — trade rejected, reason shown to trader",
        # Other: Warning shown, trade proceeds with caution flag
    }
    
    # Example: Max daily drawdown hook
    # Fires on PreTradeSubmit
    # Checks: current_daily_pnl + potential_loss > max_daily_drawdown
    # If yes: exit 2 (BLOCK) with message "Daily drawdown limit reached"
    # If no: exit 0 (PASS)
```

**The Stop Hook for Trade Verification**: When the Decision Domain says "approve," a Stop hook can force re-verification: "Are you sure? The Truth Domain showed absorption at this level 3 minutes ago." This turns a single-pass decision into a verification loop — the most powerful pattern for preventing bad trades.

---

## 7. The Sub-Agent Pattern for Domain Specialization

**Claude Code Pattern**: 15-step sub-agent lifecycle with 7 built-in agent types. Sub-agents default to `bubble` mode (escalate decisions to parent).

**ORACLE Application**: Each domain becomes a sub-agent with its own context, tools, and permission scope.

| Domain | Agent Type | Permission Mode | Tools |
|--------|-----------|----------------|-------|
| Knowledge | Read-only | `plan` | Document search, embedding lookup |
| Research | Full | `default` | Backtesting, code generation, Monte Carlo |
| Signal | Read-only | `plan` | Chart analysis, indicator calculation |
| Session | Read-only | `plan` | Time classification |
| State | Read-only | `plan` | State machine transition |
| Truth | Read-only | `plan` | L2 data, options flow, event calendar |
| Decision | Synthesis | `bubble` | Consumes all domain outputs, escalates to Risk |
| Risk | Sovereign | `bypass` (for vetoes) | Can override any other domain |
| Execution | Write | `semi_automatic` or `full_automatic` | Order placement, position management |
| Memory | Write | `dontAsk` | Trade journal, memory files |

**The `bubble` mode for Decision Domain**: The Decision Domain cannot approve its own trades. It must escalate to Risk Governance, which has the final say. This prevents the Decision Domain from becoming a god object that bypasses safety checks.

---

## 8. The Fork Agent Pattern for Parallel Market Analysis

**Claude Code Pattern**: Fork agents share 99.75% of their prompt prefix with the parent, getting a 90% cache discount. Byte-identical prefix threading makes parallel dispatch economically viable.

**ORACLE Application**: When analyzing a candidate setup, ORACLE needs to query multiple domains simultaneously. Without the fork pattern, each domain query pays full token cost.

```python
class OracleForkDispatch:
    """Parallel domain analysis using fork agent pattern."""
    
    async def analyze_parallel(self, market_context: MarketContext) -> list:
        """Fork 4 domain agents sharing the same market context prefix."""
        
        # All 4 agents share the same system prompt + market context (99%+ overlap)
        # Only the domain-specific instruction differs (~200 tokens each)
        # With prompt caching: $4.00 → $0.50 per analysis cycle
        
        results = await asyncio.gather(
            self.fork_agent("session", market_context, "Classify the current session"),
            self.fork_agent("range", market_context, "Classify range context"),
            self.fork_agent("state", market_context, "Classify market state"),
            self.fork_agent("liquidity", market_context, "Analyze liquidity structure"),
        )
        return results
    
    def fork_agent(self, domain: str, context: MarketContext, instruction: str):
        """Spawn a fork agent with byte-identical prefix."""
        # 3 frozen layers (from Claude Code):
        # 1. System prompt: parent's rendered prompt, NOT recomputed
        # 2. Tool definitions: parent's exact tool array (preserves byte identity)
        # 3. Market context: shared via constant placeholder results
        pass
```

**Why this matters**: ORACLE's Live Market Flow has 4 domains (Session, Range, State, Liquidity) that can run in parallel at step 2-5. Without fork agents, this costs 4x. With fork agents, it costs ~1.1x. Over thousands of analysis cycles per day, this is the difference between viable and prohibitively expensive.

---

## 9. The Two-Tier State Architecture for Market State

**Claude Code Pattern**: Mutable singleton `STATE` (~80 fields) for infrastructure + minimal reactive store `AppState` (34 lines) for UI.

**ORACLE Application**: Separate market infrastructure state from UI-reactive state.

| Tier | ORACLE Equivalent | Fields | Mutability |
|------|-------------------|--------|-----------|
| **Tier 1: Infrastructure** | `MARKET_STATE` singleton | Account balance, positions, daily P&L, session timers, API connections, prop firm counters | Set at startup, mutated by execution events only |
| **Tier 2: Reactive** | `DashboardState` store | Current signals, domain outputs, chart overlays, alert queue, trade approval dialogs | Changes constantly, drives UI re-renders |

**Sticky Latches for ORACLE**: Once a condition becomes true, it never reverts (prevents cache-busting in LLM prompts).

| Latch | Purpose |
|-------|---------|
| `hasActivatedPropFirmMode` | Once prop firm rules are loaded, they stay in the prompt |
| `hasConnectedL2Feed` | Once L2 data is available, Truth Domain instructions stay loaded |
| `hasOpenPosition` | Once a position is open, position management instructions stay loaded |
| `hasTriggeredRecovery` | Once recovery mode activates, reduced-risk instructions persist |

---

## 10. The Bootstrap Pipeline for Market Open

**Claude Code Pattern**: 5-phase bootstrap in ~300ms with module-level I/O parallelism.

**ORACLE Application**: Market open is ORACLE's bootstrap moment. Everything must be ready before the first tick.

| Phase | ORACLE Action | Budget |
|-------|--------------|--------|
| 0 | **Fast-Path**: Check if market is open. If closed, enter research mode immediately. | ~50ms |
| 1 | **Parallel I/O**: Fire broker connection, L2 feed connection, Redis warmup, and memory recall simultaneously during module imports. | ~500ms |
| 2 | **State Initialization**: Load yesterday's P&L, current positions, prop firm counters, active strategy list. Establish trust boundary (which strategies are approved for today). | ~200ms |
| 3 | **Domain Warm-Up**: Pre-compute session labels, load PDH/PDL/overnight levels, initialize state machine from pre-market data. | ~300ms |
| 4 | **Launch**: Enter the appropriate operating mode. Post-render prefetch: git-pull latest strategy genomes, check for overnight news events. | ~200ms |

**Total budget: ~1.25 seconds** from process start to first analysis cycle.

---

## 11. The Staleness System for Strategy Drift

**Claude Code Pattern**: Memories get age warnings ("47 days ago — code claims may be outdated"). Human-readable format triggers better LLM reasoning than raw timestamps.

**ORACLE Application**: Strategy Genomes and trade memories get staleness warnings.

```python
def get_strategy_staleness(strategy: StrategyGenome) -> str:
    """Warn about strategy drift based on last validation date."""
    days_since_validation = (now() - strategy.last_validated).days
    
    if days_since_validation <= 7:
        return ""  # Recently validated, no warning
    elif days_since_validation <= 30:
        return f"Strategy last validated {days_since_validation} days ago. Market regime may have shifted."
    elif days_since_validation <= 90:
        return f"WARNING: Strategy last validated {days_since_validation} days ago. Recommend re-running Monte Carlo before live deployment."
    else:
        return f"CRITICAL: Strategy last validated {days_since_validation} days ago. Must be re-validated through Research Domain before any live use."
```

**Why this matters**: A strategy that worked in Q1's trending market may fail in Q2's ranging market. The staleness system forces the Decision Domain to treat old strategies as hypotheses, not facts — exactly like Claude Code treats old memories.

---

## 12. The Background Extraction Agent for Trade Memory

**Claude Code Pattern**: A forked agent at the end of each query loop catches memories the main agent missed. Cooperative: defers when main agent already saved.

**ORACLE Application**: After each completed trade, a background agent extracts lessons.

```python
class TradeMemoryExtractor:
    """Background agent that extracts lessons from completed trades."""
    
    async def extract_after_trade(self, trade: CompletedTrade, market_context: MarketContext):
        """Runs as forked agent after each trade closes."""
        
        # Skip if main agent already wrote a memory for this trade
        if self.memory_exists_for_trade(trade.id):
            return
        
        # Analyze: What was surprising or non-obvious?
        # - Did the Truth Domain correctly predict the outcome?
        # - Did the State Domain's classification hold?
        # - Was the session behavior typical or anomalous?
        # - Did the strategy genome's edge hold in this market regime?
        
        # Only save what CANNOT be re-derived from trade data:
        # - Corrections: "L2 showed absorption but we entered anyway — bad"
        # - Insights: "This strategy works better in NY overlap than London open"
        # - Warnings: "Prop firm daily limit was within $50 — need tighter buffer"
```

---

## 13. The Snapshot Security Model for Risk Config

**Claude Code Pattern**: `captureHooksConfigSnapshot()` called once at startup. Hook config is frozen — cannot be modified at runtime.

**ORACLE Application**: Risk parameters are frozen at session start. No runtime modification of drawdown limits, position sizing rules, or prop firm thresholds.

```python
class RiskConfigSnapshot:
    """Risk configuration frozen at session start."""
    
    def __init__(self):
        self._snapshot = None
        self._frozen = False
    
    def capture(self, config: RiskConfig):
        """Called once at market open. After this, config is immutable."""
        self._snapshot = config.deep_copy()
        self._frozen = True
    
    def get(self) -> RiskConfig:
        """Returns frozen config. Cannot be modified."""
        assert self._frozen, "Risk config not yet captured"
        return self._snapshot
    
    # WHY: Prevents a scenario where a losing streak causes the system
    # to "adjust" its own risk limits to allow more aggressive trading.
    # The risk config set at session start is the risk config for the entire session.
    # To change it, you must restart the session (explicit human decision).
```

---

## 14. The Stop Hook for Trade Verification

**Claude Code Pattern**: When a Stop hook returns exit code 2, the conversation continues. This turns single-shot into goal-directed loops. "The most powerful integration point in the entire system."

**ORACLE Application**: Before any trade executes, a verification loop runs.

```python
class TradeVerificationLoop:
    """Stop hook pattern: force re-verification before execution."""
    
    async def verify_before_execute(self, decision: TradeDecision) -> bool:
        """Runs verification checks. Returns True only when ALL pass."""
        
        checks = [
            self.check_truth_domain_still_valid(decision),    # L2 data may have changed
            self.check_risk_limits_still_clear(decision),     # Another trade may have filled
            self.check_no_news_event_imminent(decision),      # Event calendar check
            self.check_spread_acceptable(decision),           # Spread may have widened
            self.check_prop_firm_still_safe(decision),        # Prop firm counters may have moved
        ]
        
        results = await asyncio.gather(*checks)
        
        for result in results:
            if not result.passed:
                # Exit code 2: BLOCK with reason
                # Decision Domain sees the reason and re-evaluates
                # This creates a verification LOOP, not a single check
                return False
        
        return True
    
    # The loop: Decision approves → Verification blocks → Decision re-evaluates
    # → Verification blocks again → Decision downgrades to signal-only
    # Maximum 3 verification rounds before forced rejection
```

---

## 15. Implementation Priority Matrix

| Priority | Pattern | ORACLE Domain | Effort | Impact |
|----------|---------|--------------|--------|--------|
| **P0** | Permission Modes (Risk Governance) | Risk, Decision | Medium | Critical — prevents unauthorized trades |
| **P0** | Snapshot Security (Risk Config) | Risk | Low | Critical — prevents self-modification of limits |
| **P0** | Hook System (PreTradeSubmit) | Risk, Execution | Medium | Critical — blocks bad trades at the gate |
| **P1** | Async Generator Loop | All Domains | High | High — clean cancellation, typed terminal states |
| **P1** | Stop Hook (Trade Verification) | Decision, Truth | Medium | High — prevents stale-data execution |
| **P1** | Sub-Agent Pattern | All Domains | High | High — domain isolation, permission scoping |
| **P1** | Memory System (4-Type Taxonomy) | Memory | Medium | High — structured trade learning |
| **P2** | Fork Agent (Parallel Analysis) | Session, Range, State, Liquidity | Medium | Medium — cost optimization for parallel domains |
| **P2** | Context Compression | Memory, All | Medium | Medium — prevents context overflow in long sessions |
| **P2** | Two-Tier State | All | Low | Medium — clean separation of infrastructure and UI |
| **P2** | Bootstrap Pipeline | All | Low | Medium — fast market-open readiness |
| **P3** | Staleness System | Research, Memory | Low | Medium — prevents strategy drift |
| **P3** | Background Extraction | Memory | Low | Low — catches missed trade lessons |

---

> **This document maps 14 proven architectural patterns from the most sophisticated production AI agent (Claude Code) to ORACLE AI's trading system. Every recommendation is grounded in battle-tested code, not theory. The patterns are ordered by implementation priority — P0 items prevent catastrophic failures, P1 items enable core functionality, P2 items optimize performance, and P3 items improve long-term learning.**
