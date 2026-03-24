# Hybrid Strategy: Trend/ORB/MTF

A TradingView indicator for futures scalping that combines Opening Range Breakout (ORB) detection, multi-timeframe trend confluence, and a real-time dashboard with volatility regime awareness.

Built by [Elias Victor, LLC](https://www.eliasvictor.com) — a trading technology and execution systems company focused on automated futures trading tools.

## Overview

This indicator is designed for ES, NQ, and related futures contracts on intraday timeframes (30 seconds to daily). It provides a rules-based framework for identifying and executing ORB breakout entries with multi-timeframe confirmation.

### Core Features

- **Per-session Opening Range Breakout (ORB)** — each session (S1 and S2) builds its own independent ORB with configurable duration and breakout buffer
- **ORB staleness expiration** — prevents stale signals over weekends and holidays
- **Signal deduplication** — one entry per direction per ORB session
- **Gap-resistant breakout detection** — filters gap-over events to ensure price actually traded through the level
- **Multi-timeframe trend matrix** — shows trend, VWAP, ORB confluence, and daily/weekly level status across five configurable timeframes
- **Selectable VWAP anchor** — choose between exchange VWAP or session-anchored VWAP that resets at each custom session open
- **Selectable MA type** — EMA or HMA, applied consistently across all chart visuals, dashboard, and signal logic
- **VIX / VXN / GVZ volatility display** — configurable regime thresholds with validation
- **Key levels section** — daily, weekly, and ORB high/low prices with proximity status
- **Optional JSON alerts** — webhook-ready payloads for automation platforms

### Dashboard

The real-time dashboard provides at-a-glance awareness of:

- Live and MTF trend state (Bull / Bear / Mixed)
- VWAP position across timeframes
- ORB breakout confluence across timeframes
- Daily and previous-day high/low proximity
- Volatility regime (VIX, VXN, GVZ) with configurable thresholds
- Current execution mode, session state, and MA type

## Instruments

Primarily designed for:

- **ES / MES** — S&P 500 E-mini / Micro E-mini
- **NQ / MNQ** — Nasdaq 100 E-mini / Micro E-mini
- **MGC** — Micro Gold Futures

Works on any instrument with volume data for VWAP calculations.

## Automation Stack

This indicator is designed to integrate with an automated execution pipeline:

```
TradingView Alerts → PickMyTrade (JSON/Webhooks) → Tradovate
```

When JSON alerts are enabled, the indicator sends structured payloads containing ticker, timeframe, signal direction, price, MA type, execution mode, and an optional routing tag. These payloads are compatible with PickMyTrade's webhook format for automated order execution on Tradovate.

**TradeSyncer** can be used to mirror trades across multiple prop firm accounts.

## Installation

1. Open TradingView and navigate to the Pine Script editor
2. Copy the contents of `hybrid_strategy.pine` into the editor
3. Click "Add to Chart"
4. Configure session times, MA settings, and dashboard preferences in the indicator settings

### Recommended First Steps

1. Set your timezone (default: America/New_York)
2. Confirm S1 session window matches your trading hours
3. Choose MA type (EMA or HMA) and lengths
4. Select VWAP anchor mode (Exchange or Session)
5. Adjust volatility regime thresholds if needed
6. Enable JSON alerts if connecting to a webhook automation platform

## Known Limitations

- **MTF VWAP** — matrix rows always use exchange VWAP regardless of the VWAP anchor setting. The Live row and signal engine use the selected anchor mode.
- **HTF trend lag** — the higher-timeframe trend confirmation updates only when a full bar completes on the selected HTF. On lower chart timeframes, this can lag by up to one full HTF bar.
- **17 `request.security` calls** — TradingView allows 40 per script. Adding more MTF rows or data feeds will approach this limit.

## Versioning

The current version is **v2.4.2**. Version numbering includes internal development iterations that were not all published separately. See [CHANGELOG.md](CHANGELOG.md) for the full history.

## Author

**Elias Victor, LLC**
© EliasVictor

## License

This project is licensed under the Mozilla Public License 2.0 — see the [LICENSE](LICENSE) file for details.
