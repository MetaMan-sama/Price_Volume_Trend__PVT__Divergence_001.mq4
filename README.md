# 📉 Price Volume Trend (PVT) Divergence Alert — `Price_Volume_Trend__PVT__Divergence_001.mq4`

> **MQL4 Script for MetaTrader 4**  
> Calculates the Price Volume Trend (PVT) oscillator and fires real-time alerts when bullish or bearish divergences emerge between PVT momentum and price action.

---

## Overview

The Price Volume Trend (PVT) indicator is a cumulative volume-based momentum oscillator that combines both **price change percentage** and **volume** into a single line. Unlike OBV (which adds or subtracts full volume), PVT adds a **proportional** fraction of volume based on the magnitude of the price move:

```
PVT = PVT_prev + ((Close - PrevClose) / PrevClose) × Volume
```

This makes PVT more sensitive to the *size* of price moves, not just their direction. When PVT and price **diverge**, it indicates that volume is not confirming the price trend — a classic early warning sign of trend exhaustion.

---

## How It Works

The script runs on a 60-second polling loop:

1. Calculates PVT for the current bar (`shift = 0`) and the previous bar (`shift = 1`)
2. Compares PVT direction against price direction:

| Signal | Price Action | PVT Action | Interpretation |
|---|---|---|---|
| **Bullish Divergence** | Price moves lower | PVT moves higher | Selling pressure weakening; potential reversal up |
| **Bearish Divergence** | Price moves higher | PVT moves lower | Buying pressure weakening; potential reversal down |

3. If divergence is detected, an alert is dispatched immediately

---

## Input Parameters

| Parameter | Default | Type | Description |
|---|---|---|---|
| `TradeSymbol` | `"EURUSD"` | string | Symbol to monitor |
| `Timeframe` | `PERIOD_H1` | ENUM_TIMEFRAMES | Timeframe for analysis |
| `LookbackPeriod` | `14` | int | Lookback window for divergence context |
| `EnableAlerts` | `true` | bool | Trigger MT4 sound alerts |
| `EnableEmail` | `false` | bool | Send email notifications |
| `EnablePush` | `false` | bool | Send push notifications to mobile |

---

## Alert Signals

```
Bullish Divergence Detected detected on EURUSD (Timeframe: PERIOD_H1)
```
```
Bearish Divergence Detected detected on EURUSD (Timeframe: PERIOD_H1)
```

All alerts are simultaneously logged to the MT4 **Experts journal**.

---

## PVT Formula Reference

```
PVT_current = ((Close_current - Close_previous) / Close_previous) × Volume_current
```

Because PVT uses proportional volume weighting, it better captures the **significance** of large-range bars compared to OBV, which treats all up/down bars identically regardless of how large the move was.

---

## PVT vs OBV — Key Differences

| Feature | PVT | OBV |
|---|---|---|
| Volume weighting | Proportional to price change % | Full volume added/subtracted |
| Sensitivity to move size | High — larger moves add more | Low — all qualifying bars equal |
| Best for | Trending markets with varied bar sizes | All market conditions |
| Divergence reliability | More refined signals | Simpler, widely used |

---

## Installation

1. Copy `Price_Volume_Trend__PVT__Divergence_001.mq4` to:
   ```
   MetaTrader 4/MQL4/Scripts/
   ```
2. Restart MT4 or right-click **Navigator** → **Refresh**
3. Drag the script onto a chart
4. Configure parameters and click **OK**

---

## Recommended Combinations

PVT divergences are most reliable when confirmed by other signals:

- **Support/Resistance** — divergence at a key level is a stronger signal
- **RSI divergence** — when both PVT and RSI diverge simultaneously, conviction increases significantly
- **Volume spike** — a divergence confirmed by unusually high RVOL often marks a turning point
- **Candlestick patterns** — pin bars, engulfing candles, or doji formations at the divergence point

---

## Requirements

- MetaTrader 4 (Build 600+)
- `#property strict` compliance (enforced)
- Volume data available for the symbol (tick volume is used for Forex)
- MT4 must remain running for continuous monitoring

---

## Disclaimer

This script is provided for **educational and informational purposes only**. Divergence signals are probabilistic and do not guarantee reversal. Volume data in Forex represents tick volume, not actual transaction volume. Always test on a demo account before live use.

---

## License

MIT License — free to use, modify, and distribute with attribution.
