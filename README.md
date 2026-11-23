
# 📊 Institutional Volume Profile Engine: Day + Week Ladder & POC Migration
**Custom Bin-Based Pine Script™ v6 Volume Profile with Live Auto-Sorted Level Ladder, Confirmed Candle-Close Breaks & Multi-Session Value Area Tracking**

---

### 1. Live Chart Overview & Custom Histogram Architecture

[මෙතනට ඔයාගේ ෆොටෝ එක Drag & Drop කරන්න]
<img width="2752" height="1536" alt="Gemini_Generated_Image_eymupveymupveymu" src="https://github.com/user-attachments/assets/be793565-58f8-4d25-8134-866ef347e673" />

Built entirely in **Pine Script™ v6** without relying on restricted built-in Volume Profile libraries, this engine calculates true row-by-row institutional volume distribution directly from OHLCV data (optimized for `15m` execution).

#### Core Volume Profile Mechanics
- **Custom Row Distribution (`48 Rows` / `70% VA`):** Spreads each candle's volume across its covered price bins to compute exact **Point of Control (POC)** and expands outward to the highest-volume neighboring rows until the **Value Area (`VAH` / `VAL`)** threshold is met.
- **Dual Histogram Rendering:** Simultaneously plots the **Previous Day (PD)** finalized volume profile alongside **Today's Developing Profile**, highlighting the POC row, Value Area rows, and exterior volume nodes in distinct institutional color themes.
- **Multi-Timeframe Key Levels:** Automatically projects and extends 7 high-probability institutional magnet levels:
  - **Previous Week (`W`):** `W VAH`, `W POC`, `W VAL`
  - **Previous Day (`PD`):** `PD VAH`, `PD POC`, `PD VAL`
  - **Developing Session:** Live `dPOC` (Today's developing Point of Control)

---

### 2. Live "VP LEVELS" Auto-Sorted Institutional Ladder Dashboard

Instead of forcing traders to scan across messy horizontal lines, the built-in **VP LEVELS Ladder** dynamically sorts all 7 institutional levels and **Live Price (`► PRICE`)** in descending price order every tick:

| Dashboard Module | Live Institutional Function |
| :--- | :--- |
| **Auto-Sorted Price Ladder** | Ranks `W VAH/POC/VAL`, `PD VAH/POC/VAL`, `dPOC`, and live `► PRICE` from top to bottom with instant `▲ above → BUY` / `▼ below → SELL` status. |
| **Composite `VP BIAS` Score** | Aggregates levels above vs. below price (e.g., `2 / 5 SELL`) to display an immediate macro directional bias. |
| **Next Up / Next Down Targets** | Automatically identifies the exact nearest **Resistance** and **Support** VP levels along with the live point/pip distance (`+3.6` / `-17.32`). |
| **Value Area Positioning** | Evaluates whether price is trading `ABOVE VAH`, `BELOW VAL`, or `INSIDE VALUE` for both Previous Day and Previous Week ranges. |
| **POC Migration Tracker** | Compares Today's developing `dPOC` against `PD POC` to detect institutional buyer/seller value migration in real time. |

---

### 3. Non-Repainting Candle-Close Break Detection & Alerts

- **Strict Candle-Close Validation (`barstate.isconfirmed`):** Level break labels (`⬆` / `⬇`) fire **only** when a candle officially closes through a VP level — eliminating intra-bar wick fakeouts and repainting.
- **Dynamic Alert Engine:** Includes both a unified real-time `alert()` payload (reporting the exact broken level and close price) and dedicated `alertcondition()` triggers for `PD VAH`, `PD VAL`, and `PD POC` crosses for automated webhook/bot integration.
