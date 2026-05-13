# ICT Master Indicator v1.0

**A comprehensive TradingView PineScript v5 indicator** combining 5 advanced modules for intraday trading on futures and forex charts.

---

## 📋 Overview

The **ICT Master Indicator** integrates:

1. **FVG Engine** — Fair Value Gap detection & visualization
2. **SMT Divergence** — Synergistic Market Timing (dual-pair correlation)
3. **50% Daily Range** — Session-based midpoint tracker
4. **Session Killzones** — Time-based trading zones (Asia, London, NY Open, NY Close)
5. **Swing Points + Equal Highs/Lows** — Multi-timeframe pivot tracking with sweep detection

---

## 🚀 Installation

1. Open **TradingView** → **Pine Script Editor**
2. Create a **New Indicator**
3. Copy the contents of `ICT_Master_Indicator.pine`
4. Save and add to your chart

---

## 📊 Module Details

### Module 1: FVG Engine
**Fair Value Gaps** — Automatic detection of 3-candle bullish and bearish gaps

| Setting | Description | Default |
|---------|-------------|---------|
| Show FVGs | Toggle module on/off | ✓ On |
| Bull Color | Bullish gap color | Green (70% opacity) |
| Bear Color | Bearish gap color | Red (70% opacity) |
| Bull Opacity | Bullish gap transparency (0–100) | 70 |
| Bear Opacity | Bearish gap transparency (0–100) | 70 |
| Box Width (1–10) | Horizontal extent (1=tight, 10=full edge) | 5 |
| Max Boxes Per Side | Max displayed per direction | 50 |

**How it works:**
- Detects when price gaps above (bullish) or below (bearish) the previous high/low
- Boxes persist until max cap is reached (oldest deleted first)
- **Not** deleted by price action — only by overflow management

---

### Module 2: SMT Divergence
**Synergistic Market Timing** — Compares pivot structures between paired instruments

| Pair | Chart | Partner | Detection |
|------|-------|---------|-----------|
| Micro | MNQ1!, MES1! | Each other | Auto-detect |
| Mini | NQ1!, ES1! | Each other | Auto-detect |
| Other | Any forex/crypto | Silent | — |

**How it works:**
- Automatically detects if chart is NQ1!/ES1! or MNQ1!/MES1!
- Compares pivot highs/lows between the two timeframes
- Displays dashed lines labeled "SMT ↑" (bullish divergence) or "SMT ↓" (bearish divergence)
- **Silent on all non-paired charts**

---

### Module 3: 50% Daily Range
**Session Midpoint Tracker** — Identifies equilibrium level based on daily open range

| Setting | Description | Default |
|---------|-------------|---------|
| Show 50% Daily Range | Toggle on/off | ✓ On |
| Session Start Hour (NY UTC-4) | Hour when session begins | 18 (6:00 PM) |
| Session Start Minute | Minute when session begins | 0 |
| Midpoint Color | Line color | Yellow |

**How it works:**
- Resets at 18:00 NY time (UTC-4) each trading day
- Tracks session high/low as new bars form
- **Live midpoint** updates every bar as range expands
- Single horizontal line labeled "EQ {price}"

---

### Module 4: Session Killzones
**Time-Based Trading Zones** — Highlights 4 major FX/futures sessions

| Session | Default Time (UTC-4) | Color | |
|---------|----------------------|-------|---|
| Asia | 20:00 – 00:00 | Purple | |
| London | 02:00 – 05:00 | Blue | |
| NY Open | 09:30 – 11:00 | Orange | |
| NY Close | 14:30 – 16:00 | Red | |

**Settings (all editable):**
- Toggle each session on/off
- Customize start/end time (hour + minute inputs)
- Choose background color per session
- All times in **UTC-4 (New York timezone)**

**How it works:**
- Background shades the chart during active killzone windows
- Timestamps converted from chart timezone to UTC-4 automatically

---

### Module 5: Swing Points + Equal Highs/Lows
**Multi-Timeframe Pivot Detection** — Tracks highs/lows across 1H, 4H, and Daily

#### Chart TF Gating (Visibility Rules)
- **1H pivots** → Visible only on charts ≤ 1 hour
- **4H pivots** → Visible only on charts ≤ 4 hours
- **Daily pivots** → Visible only on charts ≤ Daily

#### Sweep Detection & Countdown
Once a swing level is **swept** (wick crosses the price), it enters a countdown:

| Timeframe | Threshold | Countdown |
|-----------|-----------|-----------|
| 1H | high > swing_high OR low < swing_low | 5 closed 1H candles |
| 4H | high > swing_high OR low < swing_low | 4 closed 4H candles |
| Daily | high > swing_high OR low < swing_low | 3 closed Daily candles |

**After countdown expires → line disappears completely**

#### Equal Level Detection
Two swing levels are considered **equal** if:
- Exact same price, OR
- Within **15 ticks** (default, customizable)

Equal levels are marked with:
- Dashed connecting line between the two pivots
- Label: "1H Equal Highs", "4H Equal Lows", "D Equal Highs", etc.
- Color matches the equal-level color setting (default: yellow)

#### Settings per Timeframe (1H, 4H, Daily)

**1H Swings:**
| Setting | Range | Default |
|---------|-------|---------|
| Show 1H Swing Levels | On/Off | ✓ On |
| Show 1H Equal Highs/Lows | On/Off | ✓ On |
| 1H High Color | Color picker | Red |
| 1H Low Color | Color picker | Green |
| 1H Equal Level Color | Color picker | Yellow |
| 1H Line Width | 1–4 | 1 |
| 1H Line Style | solid/dashed/dotted | solid |
| 1H Pivot Left Bars | 1–50 | 10 |
| 1H Pivot Right Bars | 1–50 | 10 |
| Show 1H Labels | On/Off | ✓ On |

*(Same structure for 4H and Daily with adjusted defaults)*

**4H Swings:**
- Pivot Left/Right: default 5 bars
- Line Width: default 1

**Daily Swings:**
- Pivot Left/Right: default 3 bars
- Line Width: default 2

**Equal Level Tolerance (shared):**
- Default: 15 ticks
- Range: 0–100 ticks

---

## 🧪 Testing Checklist

### ✅ Pre-Flight Tests

**Before deploying, verify each module on these charts:**

#### Test 1: NQ1! 5-minute chart
```
Expected:
  ✓ FVG boxes appear (green bullish, red bearish)
  ✓ 1H swings visible at top/bottom of range
  ✓ Killzones background during session times
  ✓ SMT lines comparing NQ vs ES pivots
  ✓ Daily midpoint (EQ line) from 18:00 NY reset
```

#### Test 2: NQ1! 1-hour chart
```
Expected:
  ✓ All 5 modules visible
  ✓ 1H + 4H swings drawn
  ✓ Daily swings appear (darker line, width 2)
  ✓ Equal Highs/Lows marked with dashed lines & labels
```

#### Test 3: ES1! any timeframe
```
Expected:
  ✓ SMT divergence vs NQ1! (if on NQ1!, compare to ES1!)
  ✓ FVGs, Killzones, Daily Range all functional
  ✓ Swing levels work independently from NQ
```

#### Test 4: Any forex pair (5m/1H)
```
Expected:
  ✓ FVGs, Swings, Killzones functional
  ✓ SMT silent (no NQ/ES divergence lines)
  ✓ Daily midpoint resets at 18:00 NY
```

### 🔍 Module Verification

**FVG Engine:**
- [ ] Bullish gaps (high > previous high) create green boxes
- [ ] Bearish gaps (low < previous low) create red boxes
- [ ] Opacity slider (0–100) changes transparency
- [ ] Width slider (1–10) expands/contracts box rightward
- [ ] Max cap (e.g., 50) deletes oldest when exceeded
- [ ] Boxes persist during price movement (not deleted by new candles)

**SMT Divergence:**
- [ ] NQ1! chart shows dashed lines comparing to ES1!
- [ ] ES1! chart shows dashed lines comparing to NQ1!
- [ ] MNQ1! chart shows dashed lines comparing to MES1!
- [ ] MES1! chart shows dashed lines comparing to MNQ1!
- [ ] Forex/crypto pairs show NO SMT lines
- [ ] Labels read "SMT ↑" (bullish) or "SMT ↓" (bearish)

**50% Daily Range:**
- [ ] Midpoint resets at 18:00 NY time (UTC-4)
- [ ] Line updates live as H/L expands
- [ ] Label shows correct price: "EQ 4523.75"
- [ ] Editable session start time works immediately

**Killzones:**
- [ ] Asia (20:00–00:00): purple background
- [ ] London (02:00–05:00): blue background
- [ ] NY Open (09:30–11:00): orange background
- [ ] NY Close (14:30–16:00): red background
- [ ] All times in UTC-4 (NY timezone)
- [ ] Each zone can be individually toggled on/off
- [ ] Custom times update immediately

**Swing Points (1H/4H/Daily):**
- [ ] 1H swings only visible on ≤1H charts
- [ ] 4H swings only visible on ≤4H charts
- [ ] Daily swings visible on all ≤Daily charts
- [ ] Labels: "1H High", "4H Low", "D High" visible
- [ ] Sweep detected: high > swing_high or low < swing_low
- [ ] 1H sweep: line deleted after 5 closed 1H candles
- [ ] 4H sweep: line deleted after 4 closed 4H candles
- [ ] Daily sweep: line deleted after 3 closed Daily candles
- [ ] Line styling (color, width, solid/dashed/dotted) applied correctly

**Equal Highs/Lows:**
- [ ] Two levels within 15 ticks → marked as equal
- [ ] Exact same price → marked as equal
- [ ] Dashed connecting line drawn between equal pivots
- [ ] Labels: "1H Equal Highs", "4H Equal Lows", "D Equal Highs" visible
- [ ] Equal levels obey sweep + countdown deletion rules
- [ ] Equal tolerance slider adjusts detection sensitivity

---

## ⚙️ Performance & Resource Usage

| Resource | Limit | Used | Headroom |
|----------|-------|------|----------|
| `max_boxes_count` | 500 | ~100 (FVGs) | 400 |
| `max_lines_count` | 500 | ~251 (SMT + Swings + Equal + EQ) | 249 |
| `max_labels_count` | 500 | ~251 (SMT + Swings + Equal + EQ) | 249 |
| `request.security()` calls | ~40 (safe: ≤8) | 8 | Within safe limit |

**Status:** ✅ **Safe** — No resource constraints expected

---

## 🐛 Troubleshooting

### FVGs not appearing
- [ ] Check "Show FVGs" is toggled ON
- [ ] Verify chart has at least 2 prior candles (indicator needs history)
- [ ] Try resetting inputs to defaults

### SMT lines missing
- [ ] Chart must be NQ1!, ES1!, MNQ1!, or MES1! (forex pairs will be silent)
- [ ] Check "Show SMT Divergence" is ON
- [ ] Verify pair symbol (NQ ↔ ES, MNQ ↔ MES)

### Daily midpoint not resetting
- [ ] Check timezone: indicator assumes **UTC-4 (NY time)**
- [ ] Verify "Session Start Hour" = 18 (6:00 PM)
- [ ] If chart timezone differs, adjust manually

### Swing levels disappearing too quickly
- [ ] Check "Pivot Left/Right" settings are adequate (default: 10 bars for 1H)
- [ ] Verify sweep countdown is correct:
  - 1H: 5 closed candles
  - 4H: 4 closed candles
  - Daily: 3 closed candles

### Equal levels not detecting
- [ ] Ensure "Show 1H/4H/Daily Equal Highs/Lows" is toggled ON
- [ ] Check "Equal Level Tolerance": default 15 ticks
- [ ] Try increasing tolerance if levels are slightly offset

---

## 📝 Notes

- **All times are UTC-4 (New York timezone)**
- **Sweep detection uses wick-based crossing** (high > swing or low < swing)
- **Equal level detection supports exact matches OR within tolerance**
- **PineScript resource budgets are respected** — indicator is optimized for performance

---

## 📦 Files

- `ICT_Master_Indicator.pine` — Complete indicator code (ready to paste into TradingView)

---

## 🎯 Version History

- **v1.0** (2026-05-13) — Initial release
  - All 5 modules implemented
  - FVG, SMT, Daily Range, Killzones, Swings + Equal Levels
  - Full testing checklist included

---

**Built for traders who understand ICT concepts and value precision.**

Questions or feedback? Test thoroughly before live deployment.
