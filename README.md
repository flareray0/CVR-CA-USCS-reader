# CVR-CA USCS reader

TradingView Pine Script v5 indicator project for reading CVR-CA × USCS market state.

## Initial scope

- CVR_ratio / L_base / L_eff / m / m_eff visualization
- trend direction / reversal precursor
- sigma state / cost pressure / margin reserve
- short / mid / long MA overlay with ATR21 envelope
- MACD state and crossover context
- TradingView Pine v5 implementation

## Development policy

- CVR core unchanged
- additive / diff-only
- market-state reader, not a full bot replica
- designed for observation, warnings, and structured visual reading

## What This Reader Observes

- `sigma_used`, `ATR_raw`, and `sigma_eff` to compare raw range versus blended volatility state
- `Cost_proxy` and `CVR_ratio` to estimate how much market friction is eating into usable edge
- `L_base` and `L_eff` to compare the static structural allowance against dynamic regime and USCS gains
- `m` and `m_eff` to show margin reserve before and after dynamic adjustments
- `TrendScore` and `TrendLabel` to summarize directional pressure
- `ReversalScore` and `ReversalLabel` to surface fatigue, warning, and flip precursor states
- `Q_ratio` to monitor spread pressure against raw ATR
- short / mid / long MAs to read stack alignment at a glance
- `ATR21` and its envelope to gauge volatility expansion around the mid trend
- `MACD` state and crossover markers for intuitive momentum confirmation

## Reader, Not Bot Replica

This project is intentionally a reader and observer. It does not attempt to reproduce a live trading bot or execution stack. The CVR core is kept intact, while dynamic components are approximated into TradingView-friendly market-state signals.

## Pine Constraints

- Pine cannot access live order book spread, execution fees, or realized routing costs directly
- `Cost_proxy` is therefore a proxy built from configured fee, slippage, and spread inputs
- Multi-timeframe trend and theta signals are approximated with higher-timeframe EMA and momentum sampling
- Because `overlay=true` is required, the lower metrics are rendered as an on-chart dashboard lane instead of a separate pane

## Intended Use

The main purpose is market-state observation, warnings, and structured visual reading. It is not a direct execution engine and should not be treated as a complete trade decision system on its own.
