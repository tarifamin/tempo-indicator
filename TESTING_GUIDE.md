# ICT Master Indicator — Testing & Validation Guide

**Complete step-by-step testing procedures for all 5 modules**

---

## 📋 Pre-Deployment Checklist

Before using the indicator live, run through these tests to confirm all modules work correctly.

---

## Test Suite 1: FVG Engine

### Setup
- Open **NQ1! 5-minute chart**
- Attach the indicator
- Set FVG settings to defaults

### Test 1.1: Bullish FVG Detection
**Goal:** Confirm bullish gaps are detected and drawn correctly

**Steps:**
1. Look for a candle with **3-bar bullish gap** pattern:
   - Candle 1: Close > Open (bullish)
   - Candle 2: Close > Open (bullish)
   - Candle 3: Low > Candle 1 High (gap up)

2. **Verify:**
   - [ ] Green box appears between Candle 1 High and Candle 3 Low
   - [ ] Box color matches "Bull Color" setting
   - [ ] Box opacity matches "Bull Opacity" setting

**Expected Result:** ✅ Green boxes visible on every bullish gap

---

### Test 1.2: Bearish FVG Detection
**Goal:** Confirm bearish gaps are detected and drawn correctly

**Steps:**
1. Look for a candle with **3-bar bearish gap** pattern:
   - Candle 1: Close < Open (bearish)
   - Candle 2: Close < Open (bearish)
   - Candle 3: High < Candle 1 Low (gap down)

2. **Verify:**
   - [ ] Red box appears between Candle 3 High and Candle 1 Low
   - [ ] Box color matches "Bear Color" setting
   - [ ] Box opacity matches "Bear Opacity" setting

**Expected Result:** ✅ Red boxes visible on every bearish gap

---

### Test 1.3: Box Width Control
**Goal:** Verify "Box Width" slider stretches/compresses boxes horizontally

**Steps:**
1. Set "Box Width" to **1** (minimum)
   - [ ] Boxes should end near the formation bar (tight to formation)

2. Set "Box Width" to **10** (maximum)
   - [ ] Boxes should extend far to the right edge of chart

3. Adjust slider to **5** (middle)
   - [ ] Boxes should extend moderately to the right

**Expected Result:** ✅ Box width changes smoothly with slider

---

### Test 1.4: Opacity Control
**Goal:** Verify opacity sliders affect transparency

**Steps:**
1. Set "Bull Opacity" to **0**
   - [ ] Bullish boxes should be nearly invisible (fully transparent)

2. Set "Bull Opacity" to **100**
   - [ ] Bullish boxes should be fully opaque (darkest)

3. Repeat with "Bear Opacity"
   - [ ] Same effect for bearish boxes

**Expected Result:** ✅ Opacity changes are smooth and visible

---

### Test 1.5: Max Cap Management
**Goal:** Verify old boxes are deleted when max is exceeded

**Steps:**
1. Set "Max Boxes Per Side" to **5** (low value for testing)

2. Let the chart run for 30+ minutes to generate many FVGs

3. Count visible bullish boxes
   - [ ] Count should never exceed 5
   - [ ] As new boxes form, oldest disappears

4. Count visible bearish boxes
   - [ ] Count should never exceed 5

5. Return "Max Boxes Per Side" to **50** (default)
   - [ ] More boxes should become visible again

**Expected Result:** ✅ Max cap enforced per side, oldest deleted first

---

### Test 1.6: Toggle On/Off
**Goal:** Verify "Show FVGs" completely hides/shows all boxes

**Steps:**
1. Toggle "Show FVGs" **OFF**
   - [ ] All FVG boxes disappear immediately

2. Toggle "Show FVGs" **ON**
   - [ ] All FVG boxes reappear

**Expected Result:** ✅ Toggle cleanly hides/shows all boxes

---

## Test Suite 2: SMT Divergence

### Setup
- Open **NQ1! chart** (any timeframe 5m–1H)
- Attach the indicator
- Keep chart visible for 5+ minutes

### Test 2.1: Auto-Detection on NQ1!
**Goal:** Verify SMT activates automatically on NQ1! and compares to ES1!

**Steps:**
1. Confirm chart ticker is **NQ1!**

2. Look for recent pivot highs/lows on both NQ and ES (can verify on second chart)

3. **Verify:**
   - [ ] Dashed lines appear on chart (if divergence detected)
   - [ ] Line color is "Bullish SMT Color" or "Bearish SMT Color"
   - [ ] Label reads "SMT ↑" (bullish) or "SMT ↓" (bearish)

**Expected Result:** ✅ SMT lines and labels appear on NQ1! chart

---

### Test 2.2: Auto-Detection on ES1!
**Goal:** Verify SMT activates on ES1! and compares to NQ1!

**Steps:**
1. Switch to **ES1! chart** (same timeframe)

2. **Verify:**
   - [ ] SMT lines appear (comparing ES pivots to NQ pivots)
   - [ ] Lines are distinct from NQ1! chart (different pair comparison)

**Expected Result:** ✅ SMT lines appear correctly on ES1!

---

### Test 2.3: Auto-Detection on MNQ1!/MES1!
**Goal:** Verify SMT works on micro contracts

**Steps:**
1. Switch to **MNQ1! chart**

2. **Verify:**
   - [ ] SMT lines comparing MNQ to MES appear

3. Switch to **MES1! chart**

4. **Verify:**
   - [ ] SMT lines comparing MES to MNQ appear

**Expected Result:** ✅ SMT works on both NQ/ES and MNQ/MES pairs

---

### Test 2.4: Silent on Non-Paired Charts
**Goal:** Verify SMT produces NO output on forex/crypto

**Steps:**
1. Switch to a **forex pair** (e.g., EURUSD, GBPUSD)

2. **Verify:**
   - [ ] NO SMT lines appear
   - [ ] NO SMT labels appear
   - [ ] Other modules (FVGs, Swings, etc.) still work

3. Switch to a **crypto chart** (e.g., BTCUSD)

4. **Verify:**
   - [ ] NO SMT lines appear
   - [ ] Other modules still work

**Expected Result:** ✅ SMT silent on all non-paired charts

---

### Test 2.5: Toggle On/Off
**Goal:** Verify "Show SMT Divergence" hides/shows lines

**Steps:**
1. Toggle "Show SMT Divergence" **OFF** on NQ1!
   - [ ] All SMT lines disappear

2. Toggle **ON**
   - [ ] SMT lines reappear

**Expected Result:** ✅ Toggle cleanly hides/shows SMT visuals

---

## Test Suite 3: 50% Daily Range

### Setup
- Open **any chart** (futures or forex)
- Attach the indicator
- Wait for 18:00 NY time (UTC-4) to approach

### Test 3.1: Midpoint Calculation
**Goal:** Verify midpoint is calculated correctly

**Steps:**
1. At 18:00 NY, a new session starts
   - Manually note the High and Low at this moment

2. Watch the midpoint line over the next 30 minutes
   - Midpoint = (Session High + Session Low) / 2

3. **Verify:**
   - [ ] Midpoint is visually halfway between visible H/L
   - [ ] Label shows "EQ {price}" with correct decimal places

**Example:**
- Session High: 4530.00
- Session Low: 4520.00
- Expected Midpoint: 4525.00

---

### Test 3.2: Live Midpoint Update
**Goal:** Verify midpoint updates as new highs/lows form

**Steps:**
1. After 18:00 reset, watch chart for 1+ hour

2. If price makes a **new session high:**
   - [ ] Midpoint line should shift UP
   - [ ] Label price should increase

3. If price makes a **new session low:**
   - [ ] Midpoint line should shift DOWN
   - [ ] Label price should decrease

**Expected Result:** ✅ Midpoint updates live with each new extreme

---

### Test 3.3: Daily Reset at 18:00 NY
**Goal:** Verify session resets at correct time

**Steps:**
1. Watch chart approaching 18:00 NY (UTC-4)

2. At exactly 18:00 NY:
   - [ ] New "EQ" line should appear (or existing line reset)
   - [ ] Line should reset to current H/L at that moment

3. If testing manually, adjust "Session Start Hour" to a recent minute
   - [ ] Line should recalculate immediately

**Expected Result:** ✅ Reset happens at correct NY time

---

### Test 3.4: Timezone Handling
**Goal:** Verify correct conversion from chart timezone to UTC-4

**Steps:**
1. Check your **chart timezone** setting (e.g., UTC, EST, EST+5)

2. The indicator automatically converts to **UTC-4 (NY time)**
   - Verify by comparing visual reset time to known 18:00 NY mark

**Note:** If your chart is in UTC, 18:00 NY = 22:00 UTC. Adjust expectations accordingly.

**Expected Result:** ✅ Reset occurs at 18:00 NY regardless of chart timezone

---

### Test 3.5: Custom Session Start Time
**Goal:** Verify editable session times work

**Steps:**
1. Change "Session Start Hour" to **10** (10:00 AM NY)

2. Change "Session Start Minute" to **30**

3. Wait for 10:30 NY time on chart
   - [ ] New EQ line should appear
   - [ ] Midpoint should recalculate

**Expected Result:** ✅ Custom times work immediately

---

### Test 3.6: Toggle On/Off
**Goal:** Verify "Show 50% Daily Range" hides/shows line

**Steps:**
1. Toggle **OFF**
   - [ ] EQ line disappears
   - [ ] EQ label disappears

2. Toggle **ON**
   - [ ] Line reappears

**Expected Result:** ✅ Toggle cleanly hides/shows daily range

---

## Test Suite 4: Session Killzones

### Setup
- Open **any chart** 
- Attach the indicator
- Note current time and timezone

### Test 4.1: Asia Killzone (20:00–00:00 UTC-4)
**Goal:** Verify Asia session highlights correctly

**Steps:**
1. Manually calculate when 20:00 UTC-4 occurs in **your local time**
   - Example: If you're in UTC+0, then 20:00 UTC-4 = 00:00 UTC (midnight)

2. Wait for that time, or manually test by adjusting "Asia Start Hour" to current hour

3. **Verify:**
   - [ ] Background turns **purple** during 20:00–00:00 UTC-4
   - [ ] Background returns to normal after 00:00

**Expected Result:** ✅ Purple background during Asia hours

---

### Test 4.2: London Killzone (02:00–05:00 UTC-4)
**Goal:** Verify London session highlights correctly

**Steps:**
1. Manually calculate when 02:00–05:00 UTC-4 occurs in your local time

2. Wait for that time (or test by adjusting settings)

3. **Verify:**
   - [ ] Background turns **blue** during 02:00–05:00 UTC-4
   - [ ] Background returns to normal after 05:00

**Expected Result:** ✅ Blue background during London hours

---

### Test 4.3: NY Open Killzone (09:30–11:00 UTC-4)
**Goal:** Verify NY Open session highlights correctly

**Steps:**
1. This is typically during US market open (easiest to observe live)

2. **Verify:**
   - [ ] Background turns **orange** at 09:30 UTC-4
   - [ ] Stays orange until 11:00 UTC-4
   - [ ] Returns to normal after 11:00

**Expected Result:** ✅ Orange background during NY Open

---

### Test 4.4: NY Close Killzone (14:30–16:00 UTC-4)
**Goal:** Verify NY Close session highlights correctly

**Steps:**
1. Observe during US market close window

2. **Verify:**
   - [ ] Background turns **red** at 14:30 UTC-4
   - [ ] Stays red until 16:00 UTC-4
   - [ ] Returns to normal after 16:00

**Expected Result:** ✅ Red background during NY Close

---

### Test 4.5: Custom Killzone Times
**Goal:** Verify all 4 sessions accept custom times

**Steps:**
1. Pick one session (e.g., Asia)

2. Change "Asia Start Hour" to **12** (noon)

3. Change "Asia End Hour" to **14** (2:00 PM)

4. Wait for 12:00–14:00 UTC-4 (or adjust time manually)
   - [ ] Purple background appears during custom window

5. Repeat for other 3 sessions

**Expected Result:** ✅ All sessions accept custom start/end times

---

### Test 4.6: Overnight Sessions
**Goal:** Verify sessions that cross midnight work correctly

**Steps:**
1. Asia session runs 20:00 (8 PM) → 00:00 (midnight)
   - This crosses midnight, so the logic must handle overnight properly

2. At 23:00 UTC-4 (11 PM):
   - [ ] Purple background should be visible

3. At 00:30 UTC-4 (12:30 AM):
   - [ ] Purple background should be gone

4. At 23:59 UTC-4 → 00:00 UTC-4 transition:
   - [ ] Background should turn OFF at 00:00

**Expected Result:** ✅ Overnight sessions transition correctly at midnight

---

### Test 4.7: Individual Toggle
**Goal:** Verify each session can be toggled independently

**Steps:**
1. Toggle "Asia Killzone" **OFF**
   - [ ] Purple background never appears
   - [ ] Other killzones still work

2. Toggle "Asia Killzone" **ON**
   - [ ] Purple background reappears during Asia hours

3. Repeat with London, NY Open, NY Close

**Expected Result:** ✅ Each killzone can be toggled independently

---

## Test Suite 5: Swing Points + Equal Highs/Lows

### Setup
- Open **NQ1! 1-hour chart**
- Attach the indicator
- Set all swing modules to default settings
- Wait for new bar to form (for pivot confirmation)

### Test 5.1: 1H Swing High Detection
**Goal:** Verify 1H pivot highs are detected and drawn

**Steps:**
1. On 1H chart, look for a **pivot high**:
   - Current bar has highest close in last 10 bars
   - Previous 10 bars had lower highs

2. **Verify:**
   - [ ] Red horizontal line appears at that level
   - [ ] Line extends from pivot bar rightward
   - [ ] Label "1H High" appears (if enabled)
   - [ ] Line color matches "1H High Color"

**Expected Result:** ✅ 1H swing highs drawn correctly

---

### Test 5.2: 1H Sweep Detection
**Goal:** Verify sweep is detected when wick crosses swing high

**Steps:**
1. Identify a **1H swing high** line on chart

2. Wait for a candle where **high > swing_high level**

3. **Verify:**
   - [ ] Sweep is registered (no visual change yet)

4. Wait for 5 more **closed 1H candles** after sweep bar

5. **Verify:**
   - [ ] Line disappears completely after 5 candles
   - [ ] Label disappears

**Expected Result:** ✅ Swing high deleted after 5 closed 1H candles post-sweep

---

### Test 5.3: 1H Pivot Low & Sweep
**Goal:** Verify 1H pivot lows work similarly

**Steps:**
1. Identify a **pivot low** (lowest low in lookback window)

2. **Verify:**
   - [ ] Green horizontal line appears at that level
   - [ ] Label "1H Low" appears

3. Wait for candle where **low < swing_low level** (wick crosses below)

4. Wait for 5 closed 1H candles

5. **Verify:**
   - [ ] Line disappears after countdown

**Expected Result:** ✅ 1H swing lows detected and deleted correctly

---

### Test 5.4: 4H Swing Detection on 1H Chart
**Goal:** Verify 4H swings are visible on 1H chart

**Steps:**
1. On **1H chart**, look for **darker/thicker lines** (4H swings)
   - These appear at different price levels than 1H swings
   - Line width should be 1 (or custom setting)

2. **Verify:**
   - [ ] 4H swings visible
   - [ ] Labels read "4H High" / "4H Low"
   - [ ] Color matches 4H settings

**Expected Result:** ✅ 4H swings visible and labeled on 1H chart

---

### Test 5.5: 4H Sweep & Countdown
**Goal:** Verify 4H sweeps are deleted after 4 closed 4H candles

**Steps:**
1. Identify a **4H swing level**

2. Wait for candle crossing that level

3. Wait for 4 **closed 4H candles** (= roughly 16 1H candles)

4. **Verify:**
   - [ ] 4H line disappears after 4 4H candles

**Expected Result:** ✅ 4H levels deleted after correct countdown

---

### Test 5.6: Daily Swings on 1H Chart
**Goal:** Verify Daily swings appear on 1H chart

**Steps:**
1. On **1H chart**, look for **thickest lines** (Daily swings)
   - Default width: 2

2. **Verify:**
   - [ ] Daily swings visible
   - [ ] Labels read "D High" / "D Low"
   - [ ] Line width matches "Daily Line Width" setting (default 2)
   - [ ] Color matches Daily settings

**Expected Result:** ✅ Daily swings visible on 1H chart

---

### Test 5.7: Chart TF Gating
**Goal:** Verify swings only appear on appropriate timeframes

**Steps:**
1. On **5-minute chart:**
   - [ ] 1H swings visible
   - [ ] 4H swings visible
   - [ ] Daily swings visible
   - *(All visible because 5m ≤ all TFs)*

2. Switch to **4-hour chart:**
   - [ ] 1H swings NOT visible (4H > 1H)
   - [ ] 4H swings visible
   - [ ] Daily swings visible

3. Switch to **Daily chart:**
   - [ ] 1H swings NOT visible
   - [ ] 4H swings NOT visible
   - [ ] Daily swings visible

4. Switch to **4-hour chart** (again, to confirm):
   - [ ] 1H swings should be gone
   - [ ] 4H swings should be visible

**Expected Result:** ✅ Swings respect chart TF visibility rules

---

### Test 5.8: Equal Highs Detection
**Goal:** Verify two highs within 15 ticks are marked as equal

**Steps:**
1. Identify two 1H pivot highs on chart at similar prices
   - Example: One at 4523.50, another at 4523.60 (10 ticks apart)

2. **Verify:**
   - [ ] Dashed line connects the two pivots
   - [ ] Line color is "1H Equal Level Color" (default yellow)
   - [ ] Label reads "1H Equal Highs"

**Expected Result:** ✅ Equal highs detected within 15-tick tolerance

---

### Test 5.9: Equal Levels Tolerance
**Goal:** Verify tolerance slider adjusts equal detection

**Steps:**
1. Set "Equal Level Tolerance" to **0** (exact match only)
   - Only identical prices marked as equal

2. Set to **50** (wide tolerance)
   - More price levels detected as equal

3. **Verify:**
   - [ ] Increasing tolerance captures more equal levels
   - [ ] Decreasing tolerance is more restrictive

**Expected Result:** ✅ Tolerance slider affects equal detection

---

### Test 5.10: Equal Levels Obey Sweep Countdown
**Goal:** Verify equal-level lines disappear after sweeps

**Steps:**
1. Identify an "Equal Highs" dashed line

2. Wait for one of the two highs to be swept

3. Count countdown candles for that TF

4. **Verify:**
   - [ ] Equal-level line disappears after countdown
   - [ ] Line is deleted, not just hidden

**Expected Result:** ✅ Equal levels respect sweep countdown rules

---

### Test 5.11: Line Styling Per Timeframe
**Goal:** Verify line styles (solid/dashed/dotted) apply correctly

**Steps:**
1. Set "1H Line Style" to **dashed**
   - [ ] 1H swings should be dashed

2. Set "4H Line Style" to **dotted**
   - [ ] 4H swings should be dotted

3. Set "Daily Line Style" to **solid**
   - [ ] Daily swings should be solid

4. **Verify:**
   - [ ] Styles apply independently per TF
   - [ ] Styles are visually distinct on chart

**Expected Result:** ✅ Line styles applied per timeframe

---

### Test 5.12: Label Toggle
**Goal:** Verify label visibility can be toggled

**Steps:**
1. Toggle "Show 1H Labels" **OFF**
   - [ ] All "1H High" / "1H Low" labels disappear
   - [ ] Lines remain

2. Toggle **ON**
   - [ ] Labels reappear

3. Repeat for 4H and Daily

**Expected Result:** ✅ Labels can be toggled independently per TF

---

### Test 5.13: Full Module Toggle
**Goal:** Verify "Show 1H Swing Levels" hides entire TF

**Steps:**
1. Toggle "Show 1H Swing Levels" **OFF**
   - [ ] ALL 1H lines disappear
   - [ ] ALL 1H labels disappear
   - [ ] Equal 1H lines disappear

2. Toggle **ON**
   - [ ] All 1H visuals reappear

3. Repeat for 4H and Daily

**Expected Result:** ✅ Each TF can be toggled completely on/off

---

## Integration Test: All Modules Together

### Setup
- Open **NQ1! 1-hour chart**
- Attach indicator with all settings at defaults
- Let run for 2+ hours

### Test 6.1: Visual Clarity
**Verify all 5 modules are visible without overlap:**
- [ ] FVG boxes don't obscure swing lines
- [ ] SMT lines distinct from swing levels
- [ ] Killzone background doesn't hide price action
- [ ] EQ midpoint line clearly visible
- [ ] All labels readable

**Expected Result:** ✅ All modules visible and clear

---

### Test 6.2: Real-Time Updates
**Verify all modules update correctly as bars form:**
- [ ] New FVGs drawn immediately
- [ ] SMT lines update if new pivots form
- [ ] EQ midpoint shifts with new extremes
- [ ] Killzone backgrounds transition at correct times
- [ ] Swing lines created for new pivots
- [ ] Sweeps detected and coundowns progress

**Expected Result:** ✅ All modules update smoothly in real-time

---

### Test 6.3: Performance
**Verify indicator doesn't lag or cause slowdowns:**
- [ ] Chart still responsive to clicks/zoom
- [ ] No noticeable lag when new bars form
- [ ] Labels and lines render smoothly
- [ ] No flickering or redraw issues

**Expected Result:** ✅ Indicator performs well without slowdowns

---

### Test 6.4: Settings Persistence
**Verify all settings are saved and applied:**
- [ ] Change a color, it persists
- [ ] Change a number input, it applies immediately
- [ ] Change a toggle, effect is instant
- [ ] Close and reopen chart, settings remain

**Expected Result:** ✅ All settings persist correctly

---

## ✅ Final Sign-Off

Once all tests pass, indicator is **ready for live trading use**.

**Required passing tests:**
- [ ] All FVG tests (1.1–1.6)
- [ ] All SMT tests (2.1–2.5)
- [ ] All Daily Range tests (3.1–3.6)
- [ ] All Killzone tests (4.1–4.7)
- [ ] All Swing Point tests (5.1–5.13)
- [ ] All Integration tests (6.1–6.4)

**Status:** Ready for deployment ✅

---

**Testing completed:** ________________  
**Tested by:** ________________  
**Chart(s) used:** ________________  

---

*This testing guide ensures all ICT Master Indicator features work as specified before live deployment.*
