# Hybrid Strategy: Trend/ORB/MTF

A TradingView indicator for futures scalping that combines Opening Range Breakout (ORB) detection, multi-timeframe trend confluence, and a real-time dashboard with volatility regime awareness.

Built by [Elias Victor, LLC](https://www.eliasvictor.com) — a trading technology and execution systems company focused on automated futures trading tools.

## Overview

This indicator is designed for ES, MES, NQ, MNQ, GC, MGC, and related futures contracts on intraday timeframes. It provides a rules-based framework for identifying ORB breakout entries with multi-timeframe confirmation and dashboard-based trade context.

### Core Features

* **Per-session Opening Range Breakout (ORB)** — each session builds its own independent ORB with configurable duration and breakout buffer
* **ORB staleness expiration** — prevents stale signals over weekends and holidays
* **Signal deduplication** — one entry per direction per ORB session
* **Gap-resistant breakout detection** — filters gap-over events to confirm price traded through the level
* **Multi-timeframe trend matrix** — shows trend, VWAP, ORB confluence, and daily/weekly level status across five configurable timeframes
* **Prior weekly high/low awareness** — includes completed prior-week high/low context in the matrix
* **Selectable VWAP anchor** — choose between exchange VWAP or session-anchored VWAP that resets at each custom session open
* **Selectable MA type** — EMA or HMA, applied consistently across chart visuals, dashboard, and signal logic
* **Trade State row** — displays LONG BIAS / SHORT BIAS / SIT instead of direct execution-pressure language
* **VIX / VXN / GVZ volatility display** — configurable regime thresholds with compact Risk / Product / Action / Dly context
* **Execution context row** — shows execution mode, breakout buffer, MA type, gap-filter status, and active session
* **Key levels section** — daily, weekly, previous daily, previous weekly, and ORB high/low prices with proximity status
* **Optional JSON alerts** — webhook-ready payloads for automation platforms

### Dashboard

The real-time dashboard provides at-a-glance awareness of:

* Live and MTF trend state (Bull / Bear / Mixed)
* VWAP position across timeframes
* ORB breakout confluence across timeframes
* Daily, previous-day, and previous-week high/low proximity
* Trade State context: LONG BIAS / SHORT BIAS / SIT
* Volatility regime context for VIX, VXN, and GVZ
* Current execution mode, breakout buffer, gap-filter status, session state, and MA type

## Instruments

Primarily designed for:

* **ES / MES** — S&P 500 E-mini / Micro E-mini
* **NQ / MNQ** — Nasdaq 100 E-mini / Micro E-mini
* **GC / MGC** — Gold Futures / Micro Gold Futures

Works on any instrument with volume data for VWAP calculations.

## Automation Stack

This indicator is designed to integrate with an automated execution pipeline:

```text
TradingView Alerts → PickMyTrade (JSON/Webhooks) → Tradovate
```

When JSON alerts are enabled, the indicator sends structured payloads containing ticker, timeframe, signal direction, price, MA type, execution mode, and an optional routing tag. These payloads are compatible with webhook-based automation workflows.

Trade copying tools may be used separately to mirror trades across multiple accounts, depending on the trader’s platform setup and risk controls.

## Installation

1. Open TradingView and navigate to the Pine Script editor
2. Copy the contents of `hybrid_strategy.pine` into the editor
3. Click **Add to Chart**
4. Configure session times, MA settings, VWAP mode, and dashboard preferences in the indicator settings

### Recommended First Steps

1. Set your timezone
2. Confirm session windows match your trading hours
3. Choose MA type (EMA or HMA) and lengths
4. Select VWAP anchor mode (Exchange or Session)
5. Review breakout buffer and gap-filter settings
6. Adjust volatility regime thresholds if needed
7. Enable JSON alerts only if connecting to a webhook automation platform

## Known Limitations

* **MTF VWAP** — matrix rows always use exchange VWAP regardless of the VWAP anchor setting. The Live row and signal engine use the selected anchor mode.
* **HTF trend lag** — the higher-timeframe trend confirmation updates only when a full bar completes on the selected HTF. On lower chart timeframes, this can lag by up to one full HTF bar.
* **Volatility index timing** — VIX, VXN, and GVZ values are requested from daily data and should be treated as context, not execution triggers.
* **`request.security` usage** — TradingView allows a limited number of security requests per script. Adding more MTF rows or external data feeds may approach that limit.

## Versioning

The current published version is **v2.4.6a**.

This GitHub release syncs the repository with the currently published TradingView version. GitHub was previously behind at v2.4.2, so not every internal development version is represented as a separate GitHub commit.

See [CHANGELOG.md](CHANGELOG.md) for release history.

## Author

**Elias Victor, LLC**
© EliasVictor

## License

This project is licensed under the Mozilla Public License 2.0 — see the [LICENSE](LICENSE) file for details.
