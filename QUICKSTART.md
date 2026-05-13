# Quick Start Guide — ICT Master Indicator

**Get the indicator running in 5 minutes**

---

## 🚀 Installation (3 steps)

### Step 1: Copy the Code
1. Go to your `tempo-indicator` repository
2. Open `ICT_Master_Indicator.pine`
3. Select all code (Ctrl+A / Cmd+A)
4. Copy (Ctrl+C / Cmd+C)

### Step 2: Add to TradingView
1. Open **TradingView.com** → **Pine Script Editor**
2. Click **"Create Script"** → **"New Indicator"**
3. Clear default code
4. Paste the code (Ctrl+V / Cmd+V)
5. Click **"Save"** (give it a name, e.g., "ICT Master")

### Step 3: Attach to Chart
1. Open a chart (e.g., **NQ1! 1H**)
2. Click **"Indicators"** → Search for your saved indicator
3. Click to attach
4. **Done!** Indicator is now live on your chart

---

## ⚡ 30-Second Visual Check

After attaching, you should see **within 30 seconds:**

- ✅ **Green/Red boxes** (FVGs) on the chart
- ✅ **Colored background** during killzone hours (if you're in a session)
- ✅ **Horizontal lines** (swing levels) at recent pivot prices
- ✅ **Yellow line** (EQ midpoint) from today's session start
- ✅ **Dashed lines** (SMT divergence) if on NQ1!/ES1! charts

If you see these, the indicator is working. If not, check the checklist below.

---

## 🔍 Troubleshooting

### Nothing appears on chart
**Solution:**
1. Chart must have at least **2 bars of history** loaded
2. Scroll left to see older candles if chart just opened
3. Check all toggle switches in settings:
   - "Show FVGs" → ON
   - "Show SMT Divergence" → ON
   - "Show 50% Daily Range" → ON
   - "Show 1H/4H/Daily Swing Levels" → ON

### Only some modules appear
**By module:**

| Missing | Check |
|---------|-------|
| No FVGs | Scroll left; need 2+ candles. Check "Show FVGs" = ON |
| No SMT lines | Chart must be NQ1!, ES1!, MNQ1!, or MES1!. Forex shows nothing (expected) |
| No EQ midpoint | Must be after 18:00 NY time (UTC-4). Check "Show 50% Daily Range" = ON |
| No killzones | Depends on time of day. Change "Asia Start Hour" to current hour to test |
| No swing levels | Chart must be 1H or lower TF for 1H swings, 4H or lower for 4H, etc. |

### Boxes don't extend far (or too far)
- Adjust **"Box Width (1–10)"** slider
- 1 = tight to formation bar
- 10 = extends to chart edge

### Opacity too transparent/dark
- Adjust **"Bull Opacity"** and **"Bear Opacity"** (0–100)

### SMT lines on forex (shouldn't be there)
- This is **expected behavior for non-paired charts** — lines will not appear
- If you see them, ensure chart ticker is **not** NQ1!, ES1!, MNQ1!, or MES1!

### Swing levels disappearing too fast
- Increase **"Pivot Left Bars"** and **"Pivot Right Bars"** for each TF
- Default: 10 bars for 1H, 5 for 4H, 3 for Daily
- Higher values = more stable pivots

### Chart freezing or lagging
- Rare, but if happens:
  1. Remove indicator
  2. Reduce "Max Boxes Per Side" from 50 to 20
  3. Reattach

---

## 🎯 Core Settings (Most Important)

These 6 settings affect most trading decisions:

### 1. FVG Box Width
```
Current: 5 (medium)
Try: 1 (tight) or 10 (full)
Purpose: Controls how far boxes extend right
```

### 2. Daily Range Session Start
```
Current: 18:00 (6 PM NY)
Try: Adjust hour if you trade different session
Purpose: When to reset the EQ midpoint
```

### 3. Killzone Times
```
Current: Asia (20:00–00:00), London (02:00–05:00), NY (09:30–11:00, 14:30–16:00)
Try: Adjust to your timezone or preferred times
Purpose: Highlights high-impact trading windows
```

### 4. Swing Pivot Lookback
```
Current: 10 bars (1H), 5 bars (4H), 3 bars (Daily)
Try: Increase if pivots too frequent, decrease if too rare
Purpose: Sensitivity of pivot detection
```

### 5. Equal Level Tolerance
```
Current: 15 ticks
Try: 5 (strict) or 30 (loose)
Purpose: How close two levels must be to mark "equal"
```

### 6. Line Styles
```
Current: solid for 1H/4H, solid for Daily
Try: solid/dashed/dotted per TF
Purpose: Visual distinction between TF swings
```

---

## 📱 Recommended Chart Setup

For best results, use these chart configurations:

### Chart 1: Primary Trading (NQ1! or ES1!)
```
Timeframe: 1 hour
Indicator: ICT Master (all modules ON)
Purpose: See 1H + 4H + Daily swings + SMT divergence
```

### Chart 2: Secondary Reference (Same pair, 5m)
```
Timeframe: 5 minutes
Indicator: ICT Master (FVGs + Swings only)
Purpose: See intraday FVGs and exact 1H sweep timing
```

### Chart 3: Session Context (Any pair, Daily)
```
Timeframe: Daily
Indicator: ICT Master (Swings only, 4H/Daily enabled)
Purpose: See 4H/Daily structure, not cluttered with 1H
```

---

## 📊 Live Trading Workflow

### Before Market Open (18:00 NY)
1. ✅ Note the **EQ midpoint** from previous session
2. ✅ Identify key **swing highs/lows** from Daily chart
3. ✅ Mark **SMT divergence** levels (if on NQ/ES)
4. ✅ Check **killzone times** for today

### During Trading
1. ✅ Watch **FVG boxes** for recent gaps (entry/exit zones)
2. ✅ Observe **1H swings** for immediate support/resistance
3. ✅ Note **killzone backgrounds** when they activate
4. ✅ Track **sweep countdown** (how many candles since sweep)

### Sweep Management
When a swing level is **swept** (wick crosses it):
- **1H swings:** Disappear after 5 closed 1H candles
- **4H swings:** Disappear after 4 closed 4H candles
- **Daily swings:** Disappear after 3 closed Daily candles

After disappearance, the level is "cleared" and a new pivot can form there.

---

## 🛠️ Common Adjustments

### I want more FVG boxes
→ Increase **"Max Boxes Per Side"** from 50 to 100+

### I want fewer FVG boxes
→ Decrease to 20 or lower

### Swings are too cluttered
→ Increase **"Pivot Left/Right Bars"** (more stable pivots)
→ Toggle off one TF (e.g., hide 1H, keep 4H/Daily)

### I only care about Daily levels
→ Toggle OFF "Show 1H Swing Levels" and "Show 4H Swing Levels"
→ Keep only Daily ON

### Killzones don't match my timezone
→ Adjust each session's start/end **hour** and **minute**
→ Remember: all times are **UTC-4 (NY time)**

### SMT divergence too many lines
→ Increase **"Pivot Lookback (bars)"** for fewer but stronger signals

---

## 📖 Examples

### Example 1: Morning Trade Setup (NQ1! 1H)
```
10:00 AM NY opens → NY Open killzone (orange background)

Chart shows:
  - 2 recent 1H swing lows at 4520 and 4522 (within 15 ticks = marked equal)
  - Fresh 4H swing high at 4530 from overnight session
  - Bullish FVG box (green) between 4521–4525 from overnight
  - EQ midpoint at 4524 (from 18:00 yesterday)
  - SMT divergence line showing NQ > ES (bullish divergence)

Setup: Long at 4523, stop below 4520 low, target 4530 4H swing high
```

### Example 2: Afternoon Sweep (NQ1! 5m)
```
15:00 PM NY → Inside NY Close killzone (red background)

4H swing high at 4540 was formed at 12:00 PM.
Now at 15:15 PM, a candle wick touches 4540.50 (crosses 4540).

Indicator response:
  - Sweep registered
  - Line doesn't disappear yet (countdown in progress)
  - After 4 more closed 4H candles (~8 hours), line will disappear
  
Next day at 09:00 AM: Line is gone, 4H level "cleared"
```

### Example 3: Equal Levels (4H chart)
```
Today's 4H chart shows:
  - Swing high at 4525.00 (from bar 5)
  - Swing high at 4525.10 (from bar 12, 10 ticks apart)
  - Tolerance set to 15 ticks → They match!

Indicator shows:
  - Yellow dashed line connecting the two bars
  - Label: "4H Equal Highs"
  - Traders view this as a confluent resistance zone
```

---

## ⚠️ Important Notes

### Timezone Assumption
- **All times assume UTC-4 (New York / EST time)**
- If your chart is in different timezone, indicator converts automatically
- Session resets happen at 18:00 **NY time**, not your local time

### Sweep Definition
- A level is swept when **wick crosses** the price
- Not when close crosses, but when **high/low wick touches it**
- Example: Swing high at 4530, wick touches 4530.01 → **swept**

### Max Capacity
- FVGs: max 50 per side (oldest deleted when exceeded)
- Swings: no hard limit, but recommendation is keep <100 per TF
- Equal levels: auto-cleanup at 50 per TF

### No Alerts (by design)
- This indicator displays visuals only
- No audio/popup alerts
- You monitor the chart manually
- *(Can be added if requested)*

---

## 🎓 Learning Path

**New to the indicator?** Follow this progression:

### Day 1: FVGs + Killzones
- Turn OFF: SMT, Swings, Daily Range
- Turn ON: FVGs + Killzones only
- Observe gap patterns for 2 hours
- Get familiar with FVG box visual

### Day 2: Daily Range
- Turn ON: Daily Range (EQ midpoint)
- Turn OFF: Swings, SMT
- Watch how midpoint evolves throughout session
- Note reversals at EQ level

### Day 3: Swings (Daily only)
- Turn ON: Daily Swing Levels only
- Turn OFF: 1H, 4H, Equal levels
- Focus on 4H and Daily structure
- See how Daily pivots act as key support/resistance

### Day 4: Swings (All TFs) + Equal Levels
- Turn ON: 1H, 4H, Daily + Equal Highs/Lows
- Watch TF confluence
- See how equal levels cluster trades

### Day 5: SMT Divergence
- Open 2 charts: NQ1! and ES1! side-by-side
- Turn ON: SMT Divergence
- Observe when they diverge / converge
- Understand pair correlation strength

### Day 6+: Full Integration
- Use all 5 modules together
- Combine signals for higher conviction trades
- Adjust settings to match your style

---

## ✅ Ready?

**You've completed setup if:**
- [ ] Code copied to TradingView
- [ ] Indicator attached to chart
- [ ] See FVG boxes, killzone colors, swing lines, EQ line within 30 seconds
- [ ] Understand what each module does
- [ ] Ready to test per TESTING_GUIDE.md

**Next step:** Open `TESTING_GUIDE.md` and run through test suites before live trading.

---

## 🆘 Still Stuck?

Check these in order:
1. Indicator attached? Check Settings → Indicators
2. All toggles ON? Open indicator settings, scroll to each module
3. Chart has history? Scroll left to load older candles
4. Correct timeframe? 1H swings need ≤1H chart
5. Correct chart? SMT only works on NQ/ES/MNQ/MES
6. Timezone correct? Session resets at 18:00 NY (UTC-4)

If still not working, review the code in `ICT_Master_Indicator.pine` or refer to `README.md` Troubleshooting section.

---

**You're ready to trade!** 🚀

Start with one module at a time, master it, then layer in others.

Good luck.
