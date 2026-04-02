# Transferable Architecture: Claude Code Logic within the ORACLE 4-Layer Framework

> **Core Directive**: Claude Code's architectural patterns (from the 512K-line source leak and [claude-code-from-source.com](https://claude-code-from-source.com/)) must NOT replace ORACLE's foundational system. They act as the **execution engine** powering the existing **Research → Backtest → Iterate → Implement** pipeline. Every pattern below is mapped to a specific layer and a specific ORACLE domain.

---

## Table of Contents

1. [The 4-Layer Framework: How Claude's Logic Fits](#1-the-4-layer-framework-how-claudes-logic-fits)
2. [Layer 1: Research — Gathering Intelligence](#2-layer-1-research--gathering-intelligence)
3. [Layer 2: Backtest — Testing Hypotheses](#3-layer-2-backtest--testing-hypotheses)
4. [Layer 3: Iterate — Learning and Pruning](#4-layer-3-iterate--learning-and-pruning)
5. [Layer 4: Implement — Live Execution](#5-layer-4-implement--live-execution)
6. [The Coordinator: Tying All 4 Layers Together](#6-the-coordinator-tying-all-4-layers-together)
7. [AI-Systematic Strategy Pipeline](#7-ai-systematic-strategy-pipeline)
8. [Implementation Priority Matrix](#8-implementation-priority-matrix)
9. [References](#9-references)

---

## 1. The 4-Layer Framework: How Claude's Logic Fits

ORACLE's original architecture dictates a strict progression. No layer can be skipped. No trade can be placed without passing through all four layers. Claude Code's patterns provide the mechanics to execute each layer safely and efficiently.

| ORACLE Layer | Purpose | Claude Code Patterns Applied | Resulting Capability |
|--------------|---------|------------------------------|----------------------|
| **1. Research** | Gather market data, sentiment, liquidity | Sub-Agent Pattern, Context Compression, Fork Agents | Isolated domains gathering data without context bloat; parallel data collection at 90% cost reduction |
| **2. Backtest** | Test strategies against historical data | Fork Agents, ULTRAPLAN, Self-Describing Tools | Parallel Monte Carlo simulations; 30-minute cloud-based strategy proofs; fail-closed tool defaults |
| **3. Iterate** | Learn from results, prune failures | KAIROS Mode, Memory Staleness, Background Extraction, /dream | Proactive agents pruning dead strategies; nightly consolidation; automatic lesson extraction |
| **4. Implement** | Execute in live markets | Async Generator Loop, Stop Hooks, Snapshot Security, Permission Modes | 14-step Live Market Flow with hard risk blocking; frozen risk params; named operating modes |

---

## 2. Layer 1: Research — Gathering Intelligence

The Research layer activates the Knowledge, Truth, Signal, Session, Range, State, and Liquidity domains. Its job is to answer: **What is the market doing right now?**

### Sub-Agent Pattern for Domain Isolation

Each research domain runs as a separate **sub-agent** using Claude Code's 15-step lifecycle. This prevents cross-contamination — the Truth Domain (parsing news) cannot hallucinate technical signals, and the Signal Domain (detecting MSB/BOS) cannot be biased by sentiment data.

Every research sub-agent runs in **`bubble` permission mode**, meaning it cannot execute trades. It can only return data to the coordinator. If a research agent attempts a write operation, the permission system escalates to the parent, which denies it.

### 4-Layer Context Compression for Market Data

Market data is infinite. Without compression, the context window fills within minutes. Claude's compression system is applied directly:

| Compression Layer | ORACLE Application | Trigger |
|-------------------|-------------------|---------|
| **0. Tick Budget** | Cap L2 order book data at 50K chars per domain | Always active |
| **1. Signal Snip** | Replace old price action with `[snipped]` markers, preserving structure | Token count approaching limit |
| **2. Session Compact** | End-of-session summary replaces minute-by-minute logs | Session boundary |
| **3. History Collapse** | Full LLM summarization of the week's price action | Compact insufficient |

### Fork Agents for Parallel Data Collection

When the Research layer needs to simultaneously check 4 domains (Session, Range, State, Liquidity), it uses Claude's **fork agent** pattern. All 4 children share the parent's prompt cache (byte-identical prefix), turning a $4 parallel query into $0.50.

---

## 3. Layer 2: Backtest — Testing Hypotheses

The Backtest layer activates the Research Domain (strategy genomes). Its job is to answer: **Does this strategy actually work?**

### ULTRAPLAN for Strategy Generation

Before any backtest code is written, the system uses Claude's hidden **ULTRAPLAN** feature to generate the mathematical proof. The process:

1. The system offloads the strategy design to a cloud-hosted Claude Opus instance
2. Opus has up to **30 minutes** to generate the complete strategy genome (entry rules, exit rules, position sizing, risk parameters)
3. The user monitors progress via a browser interface
4. The plan must be **explicitly approved** before any backtest begins
5. If ULTRAPLAN fails, the system falls back to local planning mode

This prevents the common failure mode of backtesting a poorly-designed strategy for hours, only to discover the entry logic was flawed.

### Fork Agents for Monte Carlo Simulation

Once a strategy genome is approved, the Backtest layer uses fork agents to run parallel simulations across different market conditions. A parent agent sets up the strategy, then spawns 50 children to test against different date ranges, volatility regimes, and instrument sets. The 90% prompt cache discount makes this economically viable.

### Self-Describing Tools for Backtest Operations

Each backtest operation is a self-describing tool with Claude's fail-closed defaults:

| Tool | `isReadOnly` | `isConcurrentSafe` | Purpose |
|------|-------------|--------------------|---------| 
| `LoadHistoricalData` | `true` | `true` | Fetch OHLCV from database |
| `RunBacktest` | `true` | `true` | Execute strategy against data (read-only simulation) |
| `ScoreStrategy` | `true` | `true` | Calculate Sharpe, max drawdown, win rate |
| `WriteGenome` | `false` | `false` | Save validated strategy to genome library |
| `GenerateEA` | `false` | `false` | Generate MT5 Expert Advisor code |

The fail-closed default (`isReadOnly: false`) means any new tool is treated as a write operation until explicitly marked safe. This prevents accidental live execution during backtesting.

---

## 4. Layer 3: Iterate — Learning and Pruning

The Iterate layer activates the Memory Domain. Its job is to answer: **What did we learn, and what should we stop doing?**

### Memory Staleness System for Strategy Drift

Claude's staleness system is applied to Strategy Genomes. Every strategy file carries a timestamp. The system computes age in days and injects warnings:

- **Today/yesterday**: No warning. Strategy is fresh.
- **7-30 days**: Caveat: *"Strategy tested 14 days ago — market regime may have shifted. Verify against current volatility before deployment."*
- **30+ days**: Strong warning: *"Strategy is 47 days old — code claims may be outdated. Must re-backtest before any live deployment."*

Human-readable format (not ISO timestamps) triggers better reasoning — validated at 3/3 vs 0/3 in Claude's own evals.

### KAIROS Mode for Continuous Learning

ORACLE uses Claude's hidden **KAIROS** architecture for always-on observation:

- **Append-Only Daily Logs**: The system maintains `YYYY-MM-DD.md` logs of every trade, every signal, every domain output
- **Proactive Action**: Unlike standard Claude Code (which is reactive), KAIROS watches for patterns and triggers actions without being asked — e.g., detecting that a strategy has lost 3 consecutive trades and flagging it for review
- **Nightly `/dream` Consolidation**: A 4-phase process (Orient → Gather → Consolidate → Prune) merges redundant memories and keeps the index under 200 lines / 25K bytes

### Background Extraction Agent

After the market closes, a **forked agent** (sharing the parent's prompt cache for cost efficiency) reads the day's logs and extracts lessons into the permanent Trader Profile. Examples:

- "NFP days are too volatile for the momentum genome — 0/5 win rate on NFP Fridays"
- "EUR/USD performs best in London session with this entry pattern — 73% win rate"
- "Max drawdown exceeded 2% twice this week — reduce position sizing by 25%"

The extraction agent has a constrained tool budget: read-only access plus write access only to the memory directory. It uses a two-turn strategy (turn 1 reads in parallel, turn 2 writes in parallel) and defers when the main agent has already saved the same lesson.

---

## 5. Layer 4: Implement — Live Execution

The Implement layer activates the Execution, Decision, and Risk domains. Its job is to answer: **Should we place this trade, and how?**

### The Async Generator Loop (Live Market Flow)

The 14-step Live Market Flow is implemented as an **async generator** — not a sequential script. The loop yields state updates and only stops when it hits a terminal state.

**8 Terminal States** (the loop stops):

| State | Meaning |
|-------|---------|
| `trade_executed` | Order filled, position management begins |
| `trade_rejected` | Decision rejected by any domain |
| `risk_veto` | Risk Governance overrode all signals |
| `session_closed` | Market session ended |
| `prop_firm_halt` | Prop firm rules triggered halt |
| `max_loss_reached` | Daily drawdown limit hit |
| `manual_override` | User manually stopped |
| `system_error` | Unrecoverable error |

**5 Continuation States** (the loop continues):

| State | Meaning |
|-------|---------|
| `awaiting_confirmation` | Signal present, waiting for Truth Domain validation |
| `partial_fill` | Order partially filled, managing remainder |
| `scaling_opportunity` | Existing position, evaluating add |
| `state_transition` | Market state changing, re-evaluating |
| `recovery_mode` | Loss streak active, reduced sizing |

The generator pattern provides natural backpressure (the UI only processes signals as fast as it can render), clean cancellation (abort mid-analysis), and typed terminal states (every decision is logged with an explicit reason).

### Snapshot Security for Risk Parameters

At session start, risk parameters are **frozen into a snapshot** using Claude's `captureHooksConfigSnapshot()` pattern. The agent cannot modify them during the session:

- Maximum drawdown per day
- Maximum position size
- Maximum number of concurrent positions
- Allowed instruments
- Prop firm rules (if applicable)

The snapshot is read-only. Any attempt to modify risk parameters triggers a `PathTraversalError`-equivalent and is logged as a security event.

### Stop Hooks for Trade Verification

Before any order is sent to the broker, a **`PreToolUse` hook** fires. This is the most powerful integration point in the system. The hook:

1. Re-checks the Truth Domain (has anything changed since the signal?)
2. Verifies the spread is within acceptable limits
3. Confirms prop firm rules are not violated
4. Validates position sizing against the frozen snapshot

If any check fails, the hook returns **Exit Code 2** (blocking error). The trade is aborted, and the error message is shown to the decision agent as feedback, forcing it to explain why and potentially find a better entry.

### 7 Permission Modes (Operating Modes)

| ORACLE Mode | Claude Code Equivalent | Behavior |
|-------------|----------------------|----------|
| **Research** | `plan` (read-only) | Analyze only. All execution blocked. |
| **Advisory** | `default` (user approves) | Generate recommendations. User approves each trade. |
| **Semi-Auto** | `acceptEdits` (auto-approve safe) | Auto-execute within pre-approved parameters. Prompt for exceptions. |
| **Full Auto** | `dontAsk` (all allowed, logged) | Execute all approved strategies. Everything logged. |
| **Prop Firm** | `auto` (LLM classifier) | LLM classifier evaluates each trade against prop firm rules. |
| **Recovery** | Custom (restricted) | Reduced sizing. Loss-streak throttles. Some strategies disabled. |
| **Signal-Only** | `plan` + output | Read-only analysis with signal output. No execution. |

---

## 6. The Coordinator: Tying All 4 Layers Together

The main ORACLE brain acts as a **Coordinator** (Claude's 370-line system prompt pattern). Its core rule: **"Never delegate understanding."**

The coordinator orchestrates the 4 layers using Claude's 4 workflow phases:

| Phase | ORACLE Layer | What the Coordinator Does |
|-------|-------------|---------------------------|
| 1. Research | Layer 1 | Spawns domain workers (Truth, Signal, Session, etc.) to gather market data |
| 2. Synthesis | Layer 2 | Reads ALL domain results, forms its own market understanding, generates strategy hypotheses |
| 3. Implementation | Layer 3-4 | Dispatches backtest tasks, then execution tasks with precise parameters |
| 4. Verification | Layer 3 | Spawns verification workers to check results against the Iterate layer's memory |

**Tool Restrictions**: The coordinator can ONLY use `AgentTool` (spawn domain worker), `SendMessage` (communicate with domains), and `TaskStop` (terminate a domain). It cannot read market data directly, place trades, or modify strategies. This prevents the coordinator from bypassing the 4-layer progression.

**Communication**: Domains communicate via the **file-based mailbox system**. Each domain writes its output as a JSON file. The coordinator reads all outputs before making a decision. Broadcasting to `"*"` sends market alerts to all active domains simultaneously.

---

## 7. AI-Systematic Strategy Pipeline

This section describes how Claude's AI interprets market data, backtests strategies, filters the most profitable ones, and implements them automatically — all within the 4-layer framework.

### The Pipeline

```
[Layer 1: Research]          [Layer 2: Backtest]         [Layer 3: Iterate]         [Layer 4: Implement]
                                                                                    
 Knowledge Domain            ULTRAPLAN generates          KAIROS logs every          Async Generator Loop
 ingests academic             strategy genome              trade outcome              powers 14-step flow
 papers, books,               (30 min cloud session)                                 
 market structure                                         Background Extraction      Stop Hooks verify
                             Fork Agents run 50            extracts lessons           every trade before
 Signal Domain                parallel Monte Carlo                                    broker submission
 detects MSB/BOS              simulations                 Staleness System           
 patterns                                                  flags old strategies       Snapshot Security
                             Self-Describing Tools                                    freezes risk params
 Truth Domain                 score each strategy:        /dream consolidation       
 validates with L2,           - Sharpe ratio               merges memories            Permission Modes
 options flow,                - Max drawdown               nightly                    control execution
 sentiment                    - Win rate                                              authority
                              - Profit factor             Memory filters top 10%     
 Session/Range/State                                       strategies for live        7 Operating Modes
 domains provide              Top strategies promoted      deployment                 map to Claude's
 context                      to Layer 3 for iteration                                7 permission modes
```

### How the AI Filters Strategies

The filtering happens across Layers 2 and 3:

| Filter Stage | Layer | Criteria | Survival Rate |
|-------------|-------|----------|---------------|
| **Initial Generation** | 2 | ULTRAPLAN generates strategy genome | 100% (all generated) |
| **Monte Carlo Backtest** | 2 | Sharpe > 1.5, Max DD < 15%, Win Rate > 55% | ~20% survive |
| **Walk-Forward Validation** | 2 | Out-of-sample performance within 80% of in-sample | ~10% survive |
| **Regime Testing** | 2 | Profitable in at least 3 of 5 volatility regimes | ~5% survive |
| **Staleness Check** | 3 | Strategy backtested within last 14 days | Removes stale |
| **Memory Cross-Reference** | 3 | No contradicting lessons in Trader Profile | Removes conflicting |
| **Live Paper Trade** | 3-4 | 2-week paper trade in Signal-Only mode | ~2-3% survive |
| **Full Deployment** | 4 | Approved for live execution in Semi-Auto or Full Auto | Final survivors |

### Automated Implementation

Once a strategy survives all filters, the system automatically:

1. **Generates the MT5 Expert Advisor** (or TradingView Pine Script) using the strategy genome
2. **Deploys to the execution layer** in Semi-Auto mode (user approves first few trades)
3. **Promotes to Full Auto** after 10 consecutive trades match expected behavior
4. **Monitors continuously** via KAIROS — if the strategy deviates from backtest expectations by more than 2 standard deviations, it is automatically demoted back to Signal-Only mode for re-evaluation

---

## 8. Implementation Priority Matrix

| Priority | Pattern | ORACLE Layer | Purpose |
|----------|---------|--------------|---------|
| **P0** | Snapshot Security | 4. Implement | Hard-lock risk parameters at session start |
| **P0** | Stop Hooks (Exit 2) | 4. Implement | Block trades that violate risk limits |
| **P0** | Permission Modes | All Layers | Named operating modes control execution authority |
| **P0** | Coordinator Mode | All Layers | Orchestrate the 12 domains with "never delegate understanding" |
| **P1** | Async Generator | 4. Implement | Power the 14-step Live Market Flow with typed terminal states |
| **P1** | Sub-Agent Pattern | 1. Research | Isolate Truth and Signal gathering in bubble mode |
| **P1** | ULTRAPLAN | 2. Backtest | 30-minute cloud planning for strategy genomes |
| **P1** | Self-Describing Tools | 2. Backtest | Fail-closed defaults prevent accidental live execution |
| **P2** | Fork Agents | 1-2. Research/Backtest | 90% cheaper parallel data collection and Monte Carlo |
| **P2** | Context Compression | 1. Research | Prevent L2 data from blowing context window |
| **P2** | Staleness System | 3. Iterate | Force re-validation of old strategies |
| **P2** | Two-Tier State | All Layers | Infrastructure (positions, P&L) vs Reactive (signals, overlays) |
| **P3** | KAIROS / Dream | 3. Iterate | Nightly memory consolidation and proactive monitoring |
| **P3** | Background Extraction | 3. Iterate | Post-market lesson extraction into Trader Profile |
| **P3** | Swarm / Mailbox | All Layers | File-based inter-domain communication |

---

## 9. References

[1]: https://claude-code-from-source.com/ "Claude Code from Source — 18-chapter reverse engineering"
[2]: https://fortune.com/2026/03/26/anthropic-says-testing-mythos-powerful-new-ai-model-after-data-leak-reveals-its-existence-step-change-in-capabilities/ "Fortune — Anthropic Says Testing Mythos"
[3]: https://wavespeed.ai/blog/posts/claude-code-leaked-source-hidden-features/ "WaveSpeed AI — Claude Code Leaked Source: BUDDY, KAIROS & Every Hidden Feature Inside"
