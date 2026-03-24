# Changelog

All notable changes to this project are documented here.

## [v2.4.2] - 2026-03-23

### Added
- Per-session ORB logic for Session 1 and Session 2
- ORB max-age expiration to prevent stale signals across weekends and long gaps
- Signal deduplication using `longFired` and `shortFired`
- Gap-resistant breakout filtering via `filterGaps`
- Session VWAP mode with selectable anchor: `Exchange` or `Session`
- Dynamic JSON alerts via `alert()` for webhook automation
- Configurable JSON alert frequency
- Optional alert tag / route field
- Alert tag sanitization for JSON safety
- Configurable VIX / VXN / GVZ regime thresholds
- Threshold-order validation warning in the dashboard
- Configurable dashboard zone proximity and key-level proximity thresholds
- Tick-chart ORB documentation in notes, tooltips, and comments

### Changed
- Trend model now uses VWAP + fast/slow MA structure instead of a simpler MA-only read
- Moving average engine now supports both EMA and HMA via `maCalc()`
- MA selection is now applied consistently across chart MAs, cloud, MTF matrix, HTF confirmation, and signal logic
- Settings section renamed from `EMA Cloud Settings` to `Moving Average Settings`
- EMA 200 retained as a fixed long-term reference and relabeled as `Anchor EMA 200`
- Live dashboard row now shows `N/A` for both Trend and VWAP when session VWAP is unavailable outside session
- MTF ORB rows now show fixed-price ORB confluence against the chart ORB range
- JSON payloads now derive script labeling from centralized `VERSION` and `SCRIPT_NAME` variables
- Changelog header compressed to recent versions, with older history referenced externally

### Fixed
- Session VWAP now resets on session open and accumulates only during active session bars
- Session VWAP no longer drifts through off-session bars
- Current daily and weekly levels now use `lookahead_off`, eliminating future-data leakage present in earlier builds
- Dashboard proximity logic now includes tie-breaking for tight-range days
- Live dashboard no longer shows misleading `< VW` or `Mixed` states when session VWAP is unavailable
- ORB visuals now reuse named plots for `fill()` rather than duplicate hidden plots

### Removed
- Unused ATR reference section from the earlier script structure
- Old duplicate hidden ORB fill plots
- Hardcoded proximity thresholds in favor of configurable inputs
- Hardcoded volatility thresholds in favor of configurable inputs

### Notes
- MTF matrix VWAP rows always use exchange VWAP, even when Session VWAP is selected
- HTF confirmation uses completed HTF bars only and can lag by up to one full HTF bar
- Version numbering includes internal development iterations that were not all published individually

## [v2.1] - 2026-03-22

Initial published version.

### Features
- Opening Range Breakout (ORB) detection with configurable duration and buffer
- Multi-timeframe trend matrix (5 configurable timeframes)
- Live dashboard row with real-time forming-candle awareness
- VIX / VXN / GVZ volatility display with sentiment and magnitude labels
- Key levels section with daily, weekly, and ORB high/low proximity status
- Configurable session windows (S1 + optional S2)
- Execution mode selection (On Close vs Intrabar)
- EMA cloud with configurable lengths and colors
- EMA 200 long-term reference line
- VWAP overlay
- Daily and weekly level chart lines with toggles
- Signal labels (BUY / SELL) on breakout events
- Standard `alertcondition()` alerts for manual use
