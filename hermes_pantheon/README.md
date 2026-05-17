# LEVIATHAN AI — Hermes Pantheon Expansion

> **Status:** Additive Expansion Module
> **Parent System:** LEVIATHAN AI (Black Wealth Capital)
> **Author:** Manus AI (Council scaffold)
> **Note:** This module is **strictly additive**. It does not remove, override, or alter any existing LEVIATHAN architecture, document, or domain. It extends them.

---

## 1. Purpose

The Hermes Pantheon adds three new institutional capabilities to the existing 12-domain LEVIATHAN architecture:

1. A **Council of Specialized Methodology Subagents** that debate every trade idea from independent paradigms (Order Flow, Market Cipher, Delta/Volume Profile, Market Profile, Wyckoff/VSA, Markov regime modeling, Algo Pro, LuxAlgo, QuantPad, Jim Simons / RenTech statistical models).
2. A **Self-Evolving Knowledge Core** powered by the open-source Nous Research `hermes-agent`, ingesting the user's Obsidian vault and saving successful workflows as reusable skills.
3. An **Immutable Sovereign Risk Protocol** that the self-learning layer physically cannot modify, plus a Godmod3/Mirrorfish-style debate consensus engine and the MoonDev RBI (Research → Backtest → Implement) validation gauntlet.

All consensus ideas must pass through RBI before MEGALODON AI is ever permitted to route capital.

---

## 2. The Apex Orchestrator

**POSEIDON AI** is the top-level entity the user converses with. Poseidon carries the Claude / ØMEGA mythos logic, commands the entire Pantheon, translates user intent into system commands, and presents the final reports back to the user.

LEVIATHAN AI is no longer a "label for the entire system" — it is now a specialized agent with a powerful, previously missing role: **portfolio-level alpha and capital allocation**.

---

## 3. The Pantheon (14 Agents)

Power-ranked. Every name maps to a specific LEVIATHAN domain and a specific runtime responsibility.

### THE APEX ORCHESTRATOR
| Agent | Domain | Responsibility |
| :--- | :--- | :--- |
| **POSEIDON AI** | Apex Orchestrator / User Interface | The user's interlocutor. Carries the Claude/ØMEGA mythos logic, commands the Pantheon, translates intent into system actions, delivers final reports. |

### THE PRIMORDIAL POWERS (The Big Four)
| Agent | Domain | Responsibility |
| :--- | :--- | :--- |
| **LEVIATHAN AI** | Portfolio & Alpha | Multi-asset portfolio optimization, Kelly Criterion sizing, copula-based correlation hedging, alpha-decay monitoring, weighted Council aggregation. The institutional quant brain. |
| **TIAMAT AI** | Risk Governance (Sovereign) | Immutable, cryptographically locked risk authority. Hard caps on drawdown, leverage, heat, news embargoes. Can veto LEVIATHAN. |
| **LOCHNESS AI** | Strategy Engineering | Writes Pine Script indicators, Python bots, and MT5 EAs from Council consensus output. The deep-water creator. |
| **MEGALODON AI** | Execution / Routing | Live broker routing, TWAP/VWAP, iceberg orders, slippage minimization. The apex predator that strikes the market. |

### THE TITANS (Management & Validation)
| Agent | Domain | Responsibility |
| :--- | :--- | :--- |
| **ORCA AI** | Position Management | Manages live trades: trailing stops, partial profits, break-even logic, runner preservation, journaling. The hunter that finishes what Megalodon starts. |
| **NAUTILUS AI** | Research / RBI Lab | Runs MoonDev's Research → Backtest → Implement framework. Monte Carlo, walk-forward, regime testing, paper-trade graduation. Validates Lochness's code before it can go live. |
| **AEGIR AI** | Macro & Sentiment (WorldMonitor) | Runs the WorldMonitor adapter. Tracks 500+ news feeds, geopolitical risk, macro events. Enforces news embargoes (CPI, FOMC, NFP). |

### THE SENSORY NETWORK (The Analysts)
| Agent | Domain | Responsibility |
| :--- | :--- | :--- |
| **SCYLLA AI** | Truth (Order Book) | Tracks order flow, Bank Protocol manipulation patterns, dark pools, L2 imbalance, spoofing/absorption/exhaustion. |
| **CHARYBDIS AI** | State | Tracks Volume Profile, Auction Market Theory, liquidity vacuums, value-area shifts, single prints, day-type classification. |
| **SIREN AI** | Signal & Charting | Learns from Market Cipher, Algo Pro, LuxAlgo, QuantPad. Main job is **charting** — rendering the visual indicators and overlays the user reads. |
| **MERMAID AI** | Session & Range | Time-of-day context, opening ranges, Wyckoff phases (accumulation/distribution), session-quality scoring. |

### THE INTERFACE & INGESTION (The Servants)
| Agent | Domain | Responsibility |
| :--- | :--- | :--- |
| **TRITON AI** | Knowledge Ingestion | Runs the Nous Research `hermes-agent` core. Watches the Obsidian vault, ingests PDFs and YouTube transcripts, builds reusable skills, drafts strategy proposals. The messenger of the Pantheon. |
| **PROTEUS AI** | Visual Overlay (BB-Terminal) | Surfaces the Council's reasoning into the BB-Terminal-derived operator console (INTEL, OMON, CURV, etc.). The shape-shifter that makes the AI's thoughts visible to the human. |

---

## 4. The Decision Flow (Council Debate → RBI → Execution)

```
                    ┌─────────────────────────────────────┐
                    │ USER ↔ POSEIDON AI (Apex)           │
                    └───────────────┬─────────────────────┘
                                    │
                                    ▼
            ┌────────────────────────────────────────────────────┐
            │  TRITON (Obsidian) ─┐    ┌─ AEGIR (WorldMonitor)   │
            │                     ▼    ▼                         │
            │            ┌─── KNOWLEDGE BUS ───┐                 │
            │            ▼                      ▼                │
            │  SIREN ─ SCYLLA ─ CHARYBDIS ─ MERMAID              │
            │   (live market sensory inputs)                     │
            └─────────────────────┬──────────────────────────────┘
                                  │
                                  ▼  Council Session (Godmod3/Mirrorfish-style debate)
                    ┌─────────────────────────────────┐
                    │  LEVIATHAN AI weighs the votes  │
                    │  Computes portfolio fit + size  │
                    └───────────────┬─────────────────┘
                                    │
                                    ▼  Consensus reached?
                                  ┌─┴─┐
                                  │YES│
                                  └─┬─┘
                                    ▼
                    ┌─────────────────────────────────┐
                    │ NAUTILUS AI: MoonDev RBI Gauntlet│
                    │ Research → Backtest → Implement │
                    │ (Sharpe>1.5, DD<15%, WR>55%)    │
                    └───────────────┬─────────────────┘
                                    │
                                    ▼
                    ┌─────────────────────────────────┐
                    │ TIAMAT AI: Sovereign Risk Veto  │
                    │ (SHA-256 hash check, immutable) │
                    └───────────────┬─────────────────┘
                                    │ approved
                                    ▼
                    ┌─────────────────────────────────┐
                    │ MEGALODON AI: Routes order      │
                    │ ORCA AI: Manages the position    │
                    │ PROTEUS AI: Renders the trade UI │
                    └─────────────────────────────────┘
```

---

## 5. The Immutable Risk Protocol (Draft for User Approval)

| Rule | Value | Enforcement |
| :--- | :--- | :--- |
| Max Daily Drawdown | 3.0% of total equity | Global halt until 00:00 exchange time |
| Max Open Heat | 5.0% portfolio risk across all positions | New entries blocked |
| Max Leverage | 5x gross notional | Order rejected before broker submit |
| Correlated Exposure Cap | Max 2 positions same directional sector | 3rd entry blocked |
| News Embargo | No entries ±30 min of Tier-1 macro events | AEGIR-flagged events trigger embargo |
| Loss Streak Throttle | After 3 consecutive losers, position size cut 50% for 24h | Recovery Mode auto-engaged |

Mechanism: stored in `hermes_pantheon/risk/risk_governance.lock.yaml`. Set immutable at OS level (`chattr +i` on Linux). A separate guardian daemon hashes the file and refuses to allow MEGALODON to submit orders if the hash does not match the master.

---

## 6. Self-Learning Loop (Bounded)

1. User drops new knowledge into `hermes_pantheon/knowledge_vault/` (Obsidian-compatible Markdown).
2. **TRITON AI** parses it, chunks it, and tags it (methodology, asset class, regime).
3. New concepts route into the relevant subagent's prompt corpus (e.g., a new SMC/ICT note feeds SIREN's charting; a new Wyckoff insight feeds MERMAID).
4. **LOCHNESS AI** drafts a candidate strategy genome from the new knowledge.
5. **NAUTILUS AI** runs the RBI gauntlet.
6. Survivors graduate to paper trading, then live deployment under TIAMAT's veto.
7. Trade outcomes feed back to **ORCA AI** (memory) which informs the next Council session — the system gets sharper over time.

All learning happens **inside** the immutable risk protocol. The subagents and TRITON have read-only access to the risk file and zero ability to modify it.

---

## 7. Tech Stack (Additive — does not replace existing LEVIATHAN stack)

| Layer | Existing LEVIATHAN | Pantheon Addition |
| :--- | :--- | :--- |
| Orchestration | LangGraph, PydanticAI | + `hermes-agent` (Nous Research) for autonomous skills |
| Intelligence | DeepSeek-V3, Gemini 2.5 Flash | + provider-agnostic LLM routing through Hermes (Claude, GPT, Gemini, Ollama, etc.) |
| Backtesting | (per existing Research Domain) | + MoonDev RBI: `pandas`, `backtesting.py`, `yfinance`, `talib`, `ccxt` |
| Macro Data | (per existing Truth Domain) | + WorldMonitor adapter (`hermes_pantheon/adapters/aegir_worldmonitor.py`) |
| Operator UI | React/Next.js, Lightweight Charts | + BB-Terminal adapter (`hermes_pantheon/adapters/proteus_bbterminal.py`) |
| Knowledge Ingestion | LlamaParse | + Obsidian vault watcher (TRITON) |
| Regime Modeling | (planned) | + `hmmlearn`, `pomegranate` for NAUTILUS Markov module |

---

## 8. File Structure of This Expansion Module

```
hermes_pantheon/
├── README.md                          (this file)
├── agents/                            (one prompt+config per subagent)
│   ├── poseidon.md
│   ├── leviathan.md
│   ├── tiamat.md
│   ├── lochness.md
│   ├── megalodon.md
│   ├── orca.md
│   ├── nautilus.md
│   ├── aegir.md
│   ├── scylla.md
│   ├── charybdis.md
│   ├── siren.md
│   ├── mermaid.md
│   ├── triton.md
│   └── proteus.md
├── council/                           (debate engine)
│   └── debate_protocol.md
├── rbi/                               (MoonDev RBI scaffolding)
│   └── rbi_pipeline.md
├── adapters/                          (data and UI bridges)
│   ├── aegir_worldmonitor.md
│   └── proteus_bbterminal.md
├── risk/                              (immutable governance)
│   ├── risk_governance.lock.yaml
│   └── risk_guardian.md
└── knowledge_vault/                   (Obsidian drop point)
    └── README.md
```

---

## 9. Acknowledgements & Source Inspirations (Research Corpora, NOT Subagent Names)

The methodology subagents draw their internal logic from the following publicly available teaching sources. These are training corpora; the subagents are independently named.

| Methodology | Cited Sources |
| :--- | :--- |
| Order Flow / Bank Protocol | Masters of the Bank (YouTube) |
| Market Cipher | Crypto Face / Market Cipher Trading |
| Delta + Volume Profile | Trade With Profile, DeltaTrend |
| Market Profile / Auction Theory | Peter Steidlmayer, Jim Dalton, DeltaTrend |
| Wyckoff & VSA | Classical Wyckoff literature, SpacemanBTC (YouTube) |
| Markov / HMM Regime Modeling | Academic literature, `hmmlearn`, `pomegranate` |
| Algo Pro | Algo Pro signals service |
| LuxAlgo | LuxAlgo Premium toolkit |
| QuantPad | QuantPad TradingView suite |
| Jim Simons / RenTech | Public statistical-arb writeups, MoonDev's RBI references |
| RBI Framework | MoonDev (`moondevonyt/Harvard-Algorithmic-Trading-with-AI`) |
| Self-Evolving Core | Nous Research `hermes-agent` (open source) |

---

*This module is purely additive to the original LEVIATHAN AI architecture. Every existing domain, document, and protocol remains intact and authoritative.*
