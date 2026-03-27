# CVR-CA USCS reader

TradingView Pine Script v5 indicator project for reading CVR-CA × USCS market state.

## Initial scope

- CVR_ratio / L_base / L_eff / m / m_eff visualization
- trend direction / reversal precursor
- sigma state / cost pressure / margin reserve
- short / mid / long MA overlay on price
- custom sigma embedded into the radar overlay
- dedicated MACD pane
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
- `TrendState` to add hysteresis-based trend transitions (separate from legacy `TrendLabel`)
- `ReversalScore` and `ReversalLabel` to surface fatigue, warning, and flip precursor states
- `MarketPhaseLabel` to separate `DOWN_CONTINUATION`, `BEARISH_REBOUND`, `BASE_BUILDING`, `EARLY_UP`, and `CONFIRMED_UP`
- `RiseQualityScore` (0.0-1.0) to summarize how close the market is to stable trend continuation
- `Q_ratio` to monitor spread pressure against raw ATR
- short / mid / long MAs to read stack alignment at a glance
- embedded sigma radar to read `sigma_used`, `ATR_raw`, `sigma_eff`, and friction pressure in one place
- MACD pane to read crossover timing and histogram momentum in a dedicated window

## Reader, Not Bot Replica

This project is intentionally a reader and observer. It does not attempt to reproduce a live trading bot or execution stack. The CVR core is kept intact, while dynamic components are approximated into TradingView-friendly market-state signals.

Recent additions are aimed at separating stable rise versus bearish rebound behavior while staying additive and backward-compatible with existing reader outputs.

## Pine Constraints

- Pine cannot access live order book spread, execution fees, or realized routing costs directly
- `Cost_proxy` is therefore a proxy built from configured fee, slippage, and spread inputs
- Multi-timeframe trend and theta signals are approximated with higher-timeframe EMA and momentum sampling
- A single Pine script can render on the main chart or in its own pane, so the custom sigma radar is folded into the main overlay while MACD remains a companion pane

## Suggested Layout

- Add `CVR_CA_USCS_reader.pine` to the main chart for the price overlay, sigma radar, and reader summary
- Add `CVR_CA_USCS_macd_panel.pine` as the lower pane for momentum timing
- This keeps the layout within a two-indicator setup for TradingView free plans

## Intended Use

The main purpose is market-state observation, warnings, and structured visual reading. It is not a direct execution engine and should not be treated as a complete trade decision system on its own.
