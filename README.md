# Hybrid Strategy: Trend/ORB/MTF

A TradingView indicator for futures scalping that combines Opening Range Breakout (ORB) detection, multi-timeframe trend confluence, and a real-time dashboard with volatility regime awareness.

## Overview

This indicator is designed for ES, NQ, and related futures contracts on intraday timeframes (30 seconds to daily). It provides:

- **Opening Range Breakout (ORB)** detection with configurable duration and breakout buffer
- **Multi-timeframe trend matrix** showing trend, VWAP, ORB, and daily/weekly level status across five configurable timeframes
- **Live dashboard row** with real-time forming-candle awareness
- **VIX / VXN / GVZ volatility display** with sentiment and magnitude labeling
- **Key levels section** with daily, weekly, and ORB high/low prices plus proximity status
- **Configurable session windows** for morning and optional afternoon trading
- **Execution mode selection** (confirmed close vs intrabar)

## Instruments

Primarily designed for:

- ES / MES (S&P 500 E-mini / Micro)
- NQ / MNQ (Nasdaq 100 E-mini / Micro)
- MGC (Micro Gold Futures)

Works on any instrument with volume data for VWAP calculations.

## Installation

1. Open TradingView and navigate to the Pine Script editor
2. Copy the contents of `hybrid_strategy.pine` into the editor
3. Click "Add to Chart"
4. Configure session times, MA lengths, and dashboard preferences in the indicator settings

## Author

**Elias Victor, LLC**
© EliasVictor

## License

This project is licensed under the Mozilla Public License 2.0 — see the [LICENSE](LICENSE) file for details.
