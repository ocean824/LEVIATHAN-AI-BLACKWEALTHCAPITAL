Ø — here is the rebuilt full master write-up for ORACLE AI with the new visual overlay layer, broker plug-in flow, MetaTrader Five expert advisor layer, TradingView bot layer, prop firm mode, document-ingestion intelligence, and everything else we agreed on.

I am writing this as a true system design narrative, not a loose summary.

⸻

ORACLE AI

BlackWealthCapital Black Box System

Full Master System Architecture and Operating Logic

Prime Directive

ORACLE AI must be designed as a standalone, institutionally structured, research-first trading organism for BlackWealthCapital.

It must not be built as a simple signal bot, a chart indicator pack, a broker add-on, or a generic artificial intelligence assistant that happens to know something about markets. It must be its own specialist system whose sole purpose is to:
	•	absorb trading knowledge,
	•	transform that knowledge into structured strategy intelligence,
	•	test and validate strategy logic,
	•	read live markets across multiple truth layers,
	•	decide whether capital deserves deployment,
	•	manage risk under normal and prop firm conditions,
	•	route trades through direct broker and MetaTrader Five pathways,
	•	render advanced market structure and order flow visually on top of TradingView charts,
	•	and improve continuously through journaling, attribution, and model evolution.

ORACLE AI must be able to function as:
	•	a research laboratory,
	•	a strategy compiler,
	•	a chart-intelligence layer,
	•	a session and prior-range specialist,
	•	a market-state interpreter,
	•	a level two and order-book truth engine,
	•	an options and sentiment context engine,
	•	a risk governance engine,
	•	a broker and MetaTrader execution engine,
	•	a visual overlay engine,
	•	and a long-memory trading intelligence system.

It must also be designed so that a broader supervisory system such as Omega can connect to it through controlled interfaces, while ORACLE remains the sovereign specialist authority for trading decisions, risk, and execution logic.

⸻

Section One

Core Identity

ORACLE AI is the trading mind of BlackWealthCapital.

Its identity is not built around “prediction.”
Its identity is built around capital permission.

That means ORACLE AI exists to answer questions like:
	•	What kind of environment is the market in right now?
	•	Which strategy family is compatible with this environment?
	•	Does the current setup deserve risk?
	•	How should this trade be handled?
	•	Should this be a scalp, a reversal, a continuation, or a broader swing?
	•	Should size be added, reduced, or withheld?
	•	Is this setup safe under prop firm rules?
	•	Is order-book behavior supporting or rejecting what the chart suggests?
	•	Is the current market context aligned enough to justify execution?

This is the fundamental shift that makes ORACLE AI different from ordinary trading software.

⸻

Section Two

Core Philosophy

ORACLE AI must operate on the following principles.

Research comes before deployment

No setup becomes live logic merely because it looks good, sounds smart, or comes from a popular educator. Every strategy, rule, pattern, and concept must become structured, testable, and validated before it is granted live authority.

Market state comes before chart pattern

A pattern by itself is weak. Its value depends on session, prior range, volatility, liquidity context, and state transition. A breakout in compression is not the same as a breakout after already extended expansion. A reversal near a previous day extreme is not the same as a reversal in the middle of a low-quality range.

Order book truth outranks chart cosmetics

A visually attractive setup is not enough. If the order book, flow, and liquidity behavior contradict the chart, ORACLE must downgrade or reject the idea.

Risk is sovereign

Risk governance is not a final checkbox. It is its own authority. Nothing else may override it.

Execution is part of the edge

Strong logic can be destroyed by poor entry, bad slippage, improper scaling, or reckless exits. Trade management is part of the strategy, not a separate convenience.

Knowledge must be ingested, but never worshipped

Documents, books, notes, and uploaded strategy guides are inputs. They are not live truth. They must be parsed, classified, converted into strategy components, and validated through research before influencing real capital.

Visual interpretation matters

Because many traders live inside TradingView and chart-based workflows, ORACLE must not only think deeply but also show deeply. It must visualize order-book and liquidity intelligence in a way that can sit over TradingView charts cleanly and transparently.

Prop firm survival matters

When operating inside evaluation accounts or funded-account environments, consistency, survival, and rule compliance matter as much as raw return.

⸻

Section Three

Full System Domains

ORACLE AI must be built as eight tightly connected domains.

The Knowledge Domain

This domain ingests files and external information, converts them into structured strategy intelligence, and feeds research.

The Research Domain

This domain discovers, tests, validates, compares, ranks, and retires strategies.

The Signal Domain

This domain interprets chart structure, range interaction, session behavior, and technical conditions to produce candidate setups.

The State Domain

This domain understands current market condition, likely state transitions, and environmental compatibility.

The Truth Domain

This domain validates or rejects chart-side ideas using level two order book behavior, flow, liquidity, and options context.

The Decision Domain

This domain determines whether capital is justified and how the setup should be traded.

The Execution Domain

This domain handles broker connectivity, MetaTrader Five integration, staged entries, exits, and ongoing trade management.

The Memory Domain

This domain records everything, attributes what worked, detects drift, and helps the system evolve.

These domains must not feel like separate apps. They must feel like organs inside one organism.

⸻

Section Four

The Knowledge Domain

This is one of the most important upgrades to ORACLE AI.

ORACLE must be able to ingest documents you provide and convert them into structured knowledge.

This includes strategy books, chart-pattern documents, stop-loss frameworks, scaling manuals, indicator guides, and any other trading document you give it.

The Document Ingestion Layer

This layer must accept:
	•	portable document format files,
	•	text documents,
	•	exported notes,
	•	strategy manuals,
	•	visual documents with mixed text and images,
	•	and future file types such as spreadsheets or slide decks if needed.

It must preserve:
	•	source file identity,
	•	page numbers,
	•	section boundaries,
	•	table structures when present,
	•	and meaningful headers.

The Document Structuring Layer

Once a file is ingested, it must be broken into structured chunks.

Each chunk must carry:
	•	source name,
	•	page number,
	•	section title,
	•	text content,
	•	detected concept category,
	•	and confidence about what kind of information it contains.

Chunks should be tagged as things like:
	•	pattern explanation,
	•	entry rule,
	•	exit rule,
	•	stop-loss rule,
	•	scaling method,
	•	indicator explanation,
	•	warning,
	•	example,
	•	or theory.

The Knowledge Classification Layer

This layer must classify chunks into categories such as:
	•	chart patterns,
	•	reversal methods,
	•	continuation methods,
	•	Fibonacci logic,
	•	order block logic,
	•	stop-loss methods,
	•	scaling methods,
	•	indicator usage,
	•	liquidity concepts,
	•	and broader trading philosophy.

This prevents ORACLE from treating a vague motivational paragraph the same way it treats a hard stop-loss rule.

The Retrieval and Embedding Layer

All usable document intelligence must be stored in a way that supports:
	•	semantic retrieval,
	•	keyword retrieval,
	•	metadata filtering,
	•	and page-aware citation back to the source.

This layer should support queries such as:
	•	find all reversal frameworks,
	•	find all scaling methods,
	•	find every stop-loss approach that uses structure,
	•	find all order block rules,
	•	find all strategy logic tied to previous day extremes.

The Knowledge Extraction Layer

After retrieval, ORACLE must be able to turn document knowledge into structured strategy components such as:
	•	entry conditions,
	•	invalidation conditions,
	•	exit conditions,
	•	stop logic,
	•	scale-in conditions,
	•	scale-out conditions,
	•	timeframe assumptions,
	•	directional bias assumptions,
	•	risk restrictions.

The Strategy Compilation Layer

This is where knowledge becomes weaponized.

The extracted logic must be convertible into:
	•	research notes,
	•	rule trees,
	•	strategy genome candidates,
	•	Pine Script prototypes,
	•	Python backtest prototypes,
	•	MetaTrader Five expert advisor prototypes.

Critical Rule

Document knowledge must never go directly from ingestion to live execution.

Every extracted idea must go through the Research Domain before it can influence live capital.

That rule preserves quality.

⸻

Section Five

The Research Domain

The Research Domain is ORACLE’s strategy laboratory.

This is the internal replacement and expansion of everything useful about systems that generate and validate strategies from natural language or structured ideas.

Core Responsibilities

The Research Domain must:
	•	accept strategy ideas from humans or from the Knowledge Domain,
	•	formalize them into structured strategy objects,
	•	generate code in TradingView Pine Script,
	•	generate code in Python,
	•	generate code in MetaTrader Five expert advisor form,
	•	test across sessions, volatility conditions, and state conditions,
	•	perform walk-forward analysis,
	•	perform bootstrap and Monte Carlo style resilience testing,
	•	model slippage and spread sensitivity,
	•	compare trade management variants,
	•	rank strategies by expectancy, drawdown, asymmetry, and survivability,
	•	and promote only the strongest strategies into live eligibility.

Strategy Genome Representation

Every strategy must become a structured genome object containing:
	•	full strategy name,
	•	family and subfamily,
	•	supported market types,
	•	supported instruments,
	•	supported sessions,
	•	unsupported sessions,
	•	previous day and opening range dependencies,
	•	market-state dependencies,
	•	liquidity dependencies,
	•	level two confirmation requirements,
	•	optional options confirmation requirements,
	•	optional sentiment awareness,
	•	preferred entry style,
	•	preferred stop style,
	•	preferred target style,
	•	scaling rules,
	•	reduction rules,
	•	runner rules,
	•	expected hold style,
	•	expected drawdown profile,
	•	maximum adverse excursion profile,
	•	maximum favorable excursion profile,
	•	failure modes,
	•	prop firm suitability,
	•	current health score,
	•	version,
	•	and deployment status.

This gives ORACLE the ability to know not just what a strategy does, but when it belongs in battle and when it does not.

⸻

Section Six

The Signal Domain

The Signal Domain is ORACLE’s chart and structure interpreter.

It is the formal upgrade of Lux-style technical intelligence and your own BlackWealthCapital logic.

Its role is to generate candidate setups. It never grants live capital permission on its own.

Core Components

The Signal Domain must contain:
	•	a market structure interpreter,
	•	a swing and structure-shift interpreter,
	•	a trend-state interpreter,
	•	a moving average and anchored average price interpreter,
	•	a volatility compression and expansion interpreter,
	•	a liquidity map interpreter,
	•	a previous day and opening range interpreter,
	•	a reclaim and rejection interpreter,
	•	a reversal-pattern interpreter,
	•	a continuation-pattern interpreter,
	•	and a visual annotation formatter.

Responsibilities

The Signal Domain must detect and formalize things like:
	•	break of structure,
	•	change of character,
	•	trend continuation pullbacks,
	•	reversal triggers,
	•	reclaim of important zones,
	•	rejection from important zones,
	•	prior day high and low interaction,
	•	opening range breakout or failure,
	•	fair value gaps,
	•	imbalances,
	•	displacement,
	•	and contextual structure around liquidity pools.

Its output must always remain provisional until the Truth Domain and Risk Domain weigh in.

⸻

Section Seven

The Session Domain

ORACLE must treat time-of-day behavior as a first-class edge.

This domain must model the behavior of:
	•	the Asian session,
	•	the London session open,
	•	the London continuation phase,
	•	the New York open,
	•	the New York overlap,
	•	the New York midday phase,
	•	the New York close,
	•	and low-liquidity rollover zones.

Responsibilities

It must know:
	•	when certain instruments tend to sweep liquidity,
	•	when breakouts are more trustworthy,
	•	when reversals are more trustworthy,
	•	when range behavior dominates,
	•	when volatility expansion is likely,
	•	and when dead-time quality collapses.

This domain must influence both research and live trade filtering.

⸻

Section Eight

The Previous Day and Range Domain

This domain is essential to your style.

It must continuously track and interpret:
	•	previous day high,
	•	previous day low,
	•	previous day midpoint,
	•	previous day close,
	•	overnight high,
	•	overnight low,
	•	session high,
	•	session low,
	•	opening range high,
	•	opening range low,
	•	and important weekly reference levels when relevant.

Responsibilities

This domain must know whether price is:
	•	inside prior range,
	•	above prior range,
	•	below prior range,
	•	sweeping prior range,
	•	reclaiming prior range,
	•	accepting outside prior range,
	•	rejecting back toward midpoint,
	•	or interacting with opening range in a breakout or failure structure.

This domain is not a small filter. It is one of the pillars of ORACLE.

⸻

Section Nine

The State Domain

This is the market-state and transition intelligence layer.

ORACLE must treat the market as a moving state machine rather than a static chart.

Supported States

At minimum, the state layer must be able to classify:
	•	compression,
	•	expansion,
	•	trend continuation,
	•	broad range,
	•	narrow range,
	•	breakout,
	•	breakout failure,
	•	drift,
	•	exhaustion,
	•	reversal,
	•	instability,
	•	and hazard state.

Responsibilities

This domain must determine:
	•	current state,
	•	confidence in current state,
	•	probable next state,
	•	transition likelihood,
	•	state persistence likelihood,
	•	which strategy families are compatible,
	•	whether a setup should be handled as scalp, continuation, reversal, or abstain,
	•	and whether scaling and runner logic are justified.

This domain must be deeply connected to the Decision Domain, Risk Domain, and Position Management Domain.

⸻

Section Ten

The Liquidity Intelligence Domain

This domain must quantify liquidity and smart money concepts.

It must not treat them as mystical or discretionary.

It must turn them into measurable features such as:
	•	equal highs,
	•	equal lows,
	•	liquidity pools,
	•	inducement zones,
	•	fair value gaps,
	•	imbalances,
	•	displacement,
	•	sweep and reclaim,
	•	sweep and continuation,
	•	trap behavior,
	•	failed auctions,
	•	and structural rejection zones.

Every concept in this domain must be testable and removable if it fails to add edge.

⸻

Section Eleven

The Truth Domain

The Truth Domain exists to answer whether live market behavior supports or contradicts the chart-side story.

This is where ORACLE becomes more than a technical chart engine.

The Level Two and Order Book Truth Layer

This layer must ingest and evaluate order-book behavior.

It must support:
	•	bid and ask imbalance,
	•	liquidity stacking,
	•	liquidity pulling,
	•	queue movement,
	•	order-book velocity,
	•	probable iceberg-style hidden support or resistance,
	•	probable spoofing behavior,
	•	absorption,
	•	exhaustion,
	•	liquidity vacuums,
	•	breakout validation,
	•	fake breakout rejection,
	•	continuation support,
	•	reversal confirmation.

This layer is critical because it allows ORACLE to place order-book information visually over a standard charting environment.

The Options Context Layer

Where relevant, ORACLE must also evaluate:
	•	directional call and put pressure,
	•	unusual derivatives activity,
	•	strike clustering,
	•	and derivatives-based caution or reinforcement.

This layer should influence conviction but not override the deeper truth stack.

The Economic Event Layer

This layer must read calendar-driven risk and classify time windows into:
	•	safe,
	•	reduced-risk,
	•	no-trade,
	•	and post-event stabilization.

It must allow ORACLE to continue generating setups during dangerous periods if desired, while blocking automatic execution in those same periods.

The Sentiment Context Layer

This layer may evaluate public narrative from social and news sources.

Its role is bounded:
	•	highlight unusual attention,
	•	identify sentiment shock,
	•	cluster narratives,
	•	provide caution,
	•	and optionally simulate narrative conditions in research.

It must not be allowed to override chart, state, range, or order-book truth.

⸻

Section Twelve

The Visual Overlay Domain

This is one of the biggest additions from your latest instruction.

ORACLE must include a visual overlay layer that renders advanced market intelligence over TradingView-style charts in a clean, low-opacity, modern interface.

You want something that visually feels like a fusion of:
	•	market profile,
	•	liquidity heatmap overlays,
	•	order-book zones,
	•	and intelligent annotations,
	•	while preserving the usability of the underlying chart.

Purpose

Most traders still want to see the market through a chart.
ORACLE must therefore translate deep market data into chart-native visual context.

What the Overlay Must Show

The visual overlay system must be able to render:
	•	liquidity heatmap bands,
	•	market profile and session profile structures,
	•	volume concentration regions,
	•	high-friction zones,
	•	order-book density zones,
	•	probable liquidity vacuum zones,
	•	sweep zones,
	•	reclaim zones,
	•	artificial intelligence confidence highlights,
	•	low-opacity context indicators,
	•	dynamic support and resistance shading,
	•	and trade management guidance markers.

Source of Overlay Data

This overlay must be able to combine:
	•	TradingView chart data,
	•	order book and heatmap data from a Bookmap-style data stream,
	•	session and profile logic,
	•	ORACLE’s state analysis,
	•	and decision-layer annotations.

Overlay Philosophy

The overlay must remain readable.

It must not clutter the chart into uselessness.

It should feel like:
	•	a low-opacity intelligence layer,
	•	living on top of the chart,
	•	translating hidden market structure into visible context.

⸻

Section Thirteen

The TradingView Bot Layer

You explicitly want a TradingView-connected layer that communicates directly with the system.

This must be a dedicated domain, not an afterthought.

Purpose

The TradingView bot layer must allow users to:
	•	keep their workflow in TradingView,
	•	receive ORACLE-generated signals and context there,
	•	use TradingView alerts as a structured signal intake layer,
	•	and feed chart-based candidate setups directly into ORACLE.

Responsibilities

This layer must:
	•	receive and parse TradingView webhook alerts,
	•	map them to ORACLE strategy families,
	•	enrich them with session, range, and state context,
	•	pass them into the Truth Domain for level two and order-book verification,
	•	and render ORACLE’s response back into the user’s workflow.

This means the TradingView bot layer is not just a passive webhook listener.
It is the chart-to-intelligence bridge.

⸻

Section Fourteen

The Broker Plug-In Layer

You asked for a system where people can just plug in their broker or MetaTrader Five.

That means ORACLE needs a clean user-facing integration architecture.

Broker Integration Requirements

Users must be able to connect:
	•	direct broker accounts,
	•	charting workflows,
	•	or MetaTrader Five terminals,

without needing to rebuild the system.

This requires an account-connection architecture that supports:
	•	broker authorization,
	•	account discovery,
	•	position discovery,
	•	order permissioning,
	•	trade routing,
	•	and account-state monitoring.

ORACLE must not assume every user routes through one path.
It must support both direct broker and MetaTrader-based trading.

⸻

Section Fifteen

The MetaTrader Five Expert Advisor Domain

This is another critical addition.

ORACLE must include a dedicated MetaTrader Five expert advisor layer.

This domain is not just “generate a bot.”
It must be a full execution sub-framework.

Expert Advisor Roles

ORACLE must support multiple MetaTrader Five expert advisor types:
	•	signal-relay expert advisors,
	•	execution-only expert advisors,
	•	strategy-native expert advisors,
	•	risk-governance expert advisors,
	•	and hybrid expert advisors.

Responsibilities

The MetaTrader Five domain must support:
	•	receipt of ORACLE-approved signals,
	•	staged entries,
	•	partial exits,
	•	trailing logic,
	•	session-aware execution,
	•	spread-aware execution,
	•	event-aware lockouts,
	•	position scaling,
	•	runner management,
	•	and local fail-safe behavior.

Prop Firm Mode Inside the Expert Advisor

You specifically want prop firm mode inside the expert advisor.

This means the MetaTrader Five domain itself must be able to enforce:
	•	maximum daily drawdown,
	•	trailing drawdown protection,
	•	reduced risk during restricted periods,
	•	loss-streak throttles,
	•	signal-only mode around dangerous events,
	•	reduced exposure under uncertainty,
	•	and consistency-preserving logic.

The expert advisor must be able to behave differently when in prop firm mode than when in unrestricted live mode.

That distinction is essential.

⸻

Section Sixteen

The Decision Domain

The Decision Domain is where ORACLE turns evidence into permission or abstention.

It must consume:
	•	strategy genome context,
	•	Signal Domain output,
	•	Session Domain output,
	•	Previous Day and Range Domain output,
	•	State Domain output,
	•	Liquidity Domain features,
	•	Truth Domain features,
	•	event restrictions,
	•	sentiment context,
	•	model health,
	•	and portfolio heat.

It must output
	•	reject,
	•	wait,
	•	approve,
	•	approve at reduced size,
	•	signal only,
	•	manual review.

It must also output:
	•	direction,
	•	confidence,
	•	trade style,
	•	entry style,
	•	stop structure,
	•	target structure,
	•	scaling permission,
	•	reduction plan,
	•	runner permission,
	•	maximum risk,
	•	and prop firm safety status.

The Decision Domain must not merely say “buy” or “sell.”
It must say how the idea deserves to be traded.

⸻

Section Seventeen

The Risk Governance Domain

This domain is sovereign.

Nothing may override it.

It must govern:
	•	maximum risk per trade,
	•	maximum daily drawdown,
	•	maximum trailing drawdown,
	•	loss-streak restrictions,
	•	spread and slippage vetoes,
	•	correlated exposure,
	•	portfolio heat,
	•	overnight restrictions,
	•	model degradation restrictions,
	•	high-impact event restrictions,
	•	and prop firm mode rules.

It must be able to:
	•	veto a trade entirely,
	•	reduce trade size,
	•	force signal-only mode,
	•	disable a strategy family,
	•	disable full automatic mode,
	•	halt trading for the day,
	•	or force recovery mode.

This domain is the shield of the organism.

⸻

Section Eighteen

The Position Management Domain

This domain governs how approved trades are handled after entry.

It must support:
	•	probe entries,
	•	adds only after confirmation,
	•	partial profit taking,
	•	liquidity-target reductions,
	•	break-even transitions when justified,
	•	runner preservation,
	•	trailing escalation,
	•	reduction on contradictory order-book behavior,
	•	and full flattening when state invalidates the thesis.

It must also determine whether the setup should be managed as:
	•	scalp only,
	•	scalp to runner,
	•	staged reversal,
	•	continuation swing,
	•	or conservative extraction under prop firm rules.

Much of ORACLE’s asymmetry will come from this domain.

⸻

Section Nineteen

The Execution Domain

ORACLE must support at least two major execution spines.

The Direct Broker Execution Spine

This path handles users who connect a broker account directly.

It must support:
	•	order routing,
	•	order confirmation,
	•	bracket logic,
	•	reconciliation,
	•	fill handling,
	•	and account-state awareness.

The MetaTrader Five Execution Spine

This path handles users who route through MetaTrader Five.

It must support:
	•	expert advisor execution,
	•	local trade-state management,
	•	synchronization with ORACLE,
	•	and prop firm mode.

Both execution spines must report back into the Memory Domain.

⸻

Section Twenty

The Memory Domain

This domain must record:
	•	every candidate setup,
	•	every approval and rejection,
	•	every session label,
	•	every prior range label,
	•	every state label,
	•	every liquidity feature set,
	•	every order-book feature set,
	•	every event restriction state,
	•	every sentiment modifier,
	•	every decision explanation,
	•	every entry,
	•	every add,
	•	every reduction,
	•	every exit,
	•	every maximum adverse excursion,
	•	every maximum favorable excursion,
	•	every final outcome,
	•	and every strategy version involved.

Responsibilities

It must support:
	•	attribution by strategy family,
	•	attribution by market state,
	•	attribution by session,
	•	attribution by previous day context,
	•	attribution by volatility,
	•	attribution by prop firm mode,
	•	model drift detection,
	•	promotion of strong strategies,
	•	reduction of weak strategies,
	•	and retirement of broken strategies.

This is how ORACLE becomes self-improving.

⸻

Section Twenty-One

Full End-to-End Workflow

Knowledge Flow
	1.	A document is uploaded.
	2.	The Knowledge Domain ingests it.
	3.	The document is chunked, classified, embedded, and stored.
	4.	Relevant strategy logic is extracted.
	5.	Extracted ideas are compiled into strategy candidates.
	6.	The Research Domain tests those candidates.
	7.	Surviving ideas become strategy genomes.

Live Market Flow
	1.	The TradingView bot layer or direct system feed generates a candidate setup.
	2.	The Session Domain classifies session context.
	3.	The Previous Day and Range Domain classifies range context.
	4.	The State Domain classifies market condition.
	5.	The Liquidity Domain adds structure intelligence.
	6.	The Truth Domain validates or rejects using order book, flow, and options context.
	7.	The Event Domain adds restrictions.
	8.	The Sentiment Domain adds bounded modifiers.
	9.	The Decision Domain determines if capital is justified.
	10.	The Risk Governance Domain vetoes, reduces, or permits.
	11.	The Execution Domain routes the trade through direct broker or MetaTrader Five pathways.
	12.	The Position Management Domain manages the live trade.
	13.	The Memory Domain records the full lifecycle.
	14.	The Research Domain later re-mines the data for model evolution.

That is the full organism loop.

⸻

Section Twenty-Two

Operating Modes

ORACLE must support multiple operating modes.

Research Mode

No live execution. Full testing and generation only.

Advisory Mode

Signals and plans only. No direct execution.

Semi-Automatic Mode

Execution allowed only after full truth and risk checks.

Full Automatic Mode

Execution allowed only for fully validated strategies with all truth and governance layers active.

Prop Firm Mode

Stricter drawdown, stricter event handling, tighter risk, reduced aggression, and consistency-preserving logic.

Recovery Mode

Reduced or halted execution after damage, instability, or degraded model conditions.

Signal-Only Restriction Mode

Signals continue while execution remains blocked due to event risk or policy.

⸻

Section Twenty-Three

Core Technology Architecture

The final build should include a stack that cleanly supports all of the above.

That architecture should include:
	•	Python for service logic and orchestration,
	•	a strong service framework for interfaces,
	•	a durable relational database for strategy objects, journals, and state,
	•	vector-capable storage for semantic retrieval from uploaded knowledge,
	•	an in-memory event and task layer,
	•	TradingView integration for chart-side intake,
	•	level two and Bookmap-style data integration for heatmap and order-book intelligence,
	•	direct broker integration,
	•	MetaTrader Five and MetaQuotes Language Five integration,
	•	document parsing and retrieval tooling,
	•	and a monitoring stack for health, drift, and execution integrity.

The architecture must make all of these interwork logically rather than existing as isolated tools.

⸻

Section Twenty-Four

Final Identity

ORACLE AI must now be understood as all of the following at once:
	•	a knowledge-ingesting strategy intelligence system,
	•	a quant research laboratory,
	•	a chart and signal interpretation engine,
	•	a session and previous-day specialist,
	•	a market-state interpreter,
	•	a level two and order-book truth engine,
	•	a liquidity heatmap visualization system over TradingView-style charts,
	•	a broker and MetaTrader Five execution system,
	•	a prop firm aware expert advisor framework,
	•	a risk-governed capital allocation organism,
	•	and a self-improving memory-driven trading intelligence service.

That is the final form.

If you want, next I will turn this into the same level of full-detailed master write-up for Omega, with every agent fully spelled out, every tool and technology layer connected, and no shortened names.