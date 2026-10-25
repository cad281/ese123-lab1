# ESE 123 Lab 1: DC Power Supply & Ohm's Law

**Interactive page:** https://cad281.github.io/ese123-lab1/

All labs: [Lab 1: DC Power & Ohm's Law](https://cad281.github.io/ese123-lab1/) · [Lab 2: Digital Multimeter](https://cad281.github.io/ese123-lab2/) · [Lab 3: SPICE & Soldering](https://cad281.github.io/ese123-lab3/) · [Lab 4: Function Generator & Scope](https://cad281.github.io/ese123-lab4/) · [Lab 5: Capacitors & Scope](https://cad281.github.io/ese123-lab5/) · [Lab 6: Operational Amplifiers](https://cad281.github.io/ese123-lab6/)

This guide is written by a TA for students taking ESE 123 who are new to electrical engineering. It explains **what** you do in Lab 1, **why** each step matters, and **how** to do it on the bench. The interactive page simulates the power supply and the circuits so you can predict your readings before you take them.

---

## What this lab is about

| You will… | Using… |
|---|---|
| Work out the safe power, current and voltage limits for a resistor | Pre-lab formulas (P = I²R = V²/R) |
| Learn the two operating modes of a bench supply: **constant voltage (CV)** and **constant current (CC)** | Keysight E36312A triple-output DC supply, channel 2 |
| Measure a 1 Ω resistor's current at many voltages and find its resistance from the slope | Google Sheets scatter chart + trendline |
| Show that an LED does **not** obey Ohm's law | Blue LED, channel 3, CC and CV sweeps |

## Why it matters

- **Ohm's law (V = IR)** is the most-used equation in this course. Measuring it yourself shows where it works (resistors) and where it doesn't (LEDs, diodes).
- **Every circuit you build this semester is powered by a bench supply.** Knowing CV vs CC, and always setting a current limit first, protects your parts and you.
- **Derating** (using parts below their maximum rating) is standard engineering practice. Parts run cooler, last longer and don't burn fingers.
- **Fitting a line to data** is how engineers pull one reliable number out of many slightly noisy readings.

## How to do it, step by step

### Pre-lab: safe limits
1. Our resistors are rated **¼ W**. Derate by 2 → **P_max = ⅛ W = 0.125 W**.
2. For the 1 Ω resistor: **I_max = √(P_max / R) = √(0.125 / 1) = 0.354 A** and **V_max = √(P_max · R) = 0.354 V**.
3. You will type I_max into the supply as its current limit. That limit is what keeps the resistor safe.

### Part 1: setting up the supply (steps 5–13)
1. Sign in to the lab PC with your NetID. Open a blank Google Sheet; label column A `Voltage (V)` and column B `Current (A)`.
2. Connect the **1 Ω resistor (brown-black-gold-gold)** to **channel 2** with alligator clips or mini-grabbers. Red lead to +, black to −. A resistor has no polarity.
3. Power on, press the green **channel 2** selector (top right).
4. **Set the current limit first** to I_max (0.354 A). Check the voltage setpoint is 0.
5. Press the green **ON** button under channel 2. You should read 0 V and 0 A in **CV** mode.

### Part 2: the sweep (steps 14–17)
1. Raise the voltage **0.05 V** at a time. Use the keypad once (highlight the field, type `.05`, press **Enter**; nothing happens until Enter), then the knob (slow turns = 1 mV per click; fast turns jump faster).
2. At every step record **V, I and the mode (CV/CC)** to full displayed precision.
3. Keep going until the display says **CC**. The current is now pinned at the limit and the voltage stops following the setpoint. That is the end of the sweep.
4. Turn the output **OFF**.

### Part 3: the chart (steps 18–23)
1. Select only the numbers → **Insert → Chart** → Chart type **Scatter**.
2. **Customize → Series → Trendline ✓ → Label: Use Equation**. You get `y = mx + b`.
3. **m is the conductance G in siemens (A/V). R = 1/m.** Screenshot the chart for your report.

### Part 4: the blue LED
1. Get a blue LED from your TA. **Set channel 3's voltage limit to 3.3 V first.**
2. The **long lead is the anode (+)**. Connect it to the red terminal of channel 3.
3. **CC sweep:** set the current to 5, 10, 15 and 20 mA and record V each time. Expect about **2.7–3.0 V**.
4. **CV sweep:** set the current limit back to 20 mA, then set the voltage to 0, 0.5, 1.0, 1.5, 2.0 and 2.5 V. Expect almost **zero current**, because the LED is not on yet.
5. Plot all points together with a linear trendline. Notice how badly a straight line fits.
6. **Differential resistance** Δr = ΔV/ΔI: use the two highest-voltage points (about 15 Ω) and the two lowest (enormous, because ΔI ≈ 0).
7. Show your TA both plots, clean up, and return unused parts.

## What you should observe, and why

| Observation | Why it happens |
|---|---|
| Current rises in a straight line with voltage | A resistor is **ohmic**: I = V/R with constant R. |
| Measured R is a bit above 1 Ω (often 1.05–1.10 Ω) | The supply measures at its own terminals, so the **clips, leads and contacts** (~0.05–0.1 Ω) count as part of "the resistor". That's 5–10% of 1 Ω. |
| The supply switches from CV to CC near 0.35 V | Holding the voltage would need more than the 0.354 A limit, so it holds the current instead and lets the voltage drop to I_limit × R. |
| Readings stay at 0 with the output off | The output enable button disconnects the channel; setpoints alone don't drive anything. |
| LED current is ~0 below 2.5 V, then rises steeply | An LED needs a minimum "turn-on" voltage before it conducts. Above that, current grows almost exponentially. |
| Linear trendline through LED data is a poor fit | Non-ohmic device: there is no single resistance, only Δr at a given point. |

## Formula sheet (what, when, example)

### Ohm’s law

```
V = I · R
```

**Use it when:** You know two of voltage, current and resistance for a resistor and need the third. Only works for ohmic devices (resistors), not LEDs.

- `V`: voltage across the part (V)
- `I`: current through it (A)
- `R`: resistance (Ω)

**Example:** 0.30 V across 1 Ω → I = 0.30 / 1 = 0.30 A.

### Power

```
P = I · V = I² · R = V² / R
```

**Use it when:** Checking how hot a part gets. Pick the form that uses what you know: I and V, or I and R, or V and R.

- `P`: power turned into heat (W)

**Example:** 0.354 A through 1 Ω → P = 0.354² × 1 = 0.125 W.

### Derated power limit

```
Pmax = Prated / derating factor
```

**Use it when:** Before choosing setpoints. We derate by 2 for cooler, safer, more reliable parts.

- `Prated`: manufacturer rating (¼ W for our resistors)

**Example:** ¼ W / 2 = ⅛ W = 0.125 W.

### Maximum safe current

```
Imax = √(Pmax / R)
```

**Use it when:** Setting the current limit on the supply so the resistor can never exceed Pmax.

**Example:** √(0.125 / 1) = 0.354 A for the 1 Ω resistor.

### Maximum safe voltage

```
Vmax = √(Pmax · R)
```

**Use it when:** Knowing the highest voltage you can apply in CV mode.

**Example:** 20 Ω, 5 W derated by 2: √(2.5 × 20) = 7.071 V.

### Conductance

```
G = 1 / R   (units: siemens, S = A/V)
```

**Use it when:** Reading your I-vs-V trendline. The slope m is G, so R = 1/m.

**Example:** Trendline y = 0.926x + 0.0002 → G = 0.926 S → R = 1.080 Ω.

### Supply mode (CV or CC)

```
if Vset / R ≤ Ilimit → CV, V = Vset
else → CC, I = Ilimit, V = Ilimit · R
```

**Use it when:** Predicting what the E36312A display will show, and recognising when your sweep has hit the current limit.

**Example:** Vset = 0.40 V, R = 1.07 Ω needs 0.374 A > 0.354 A → CC at 0.379 V.

### Differential resistance

```
Δr = ΔV / ΔI
```

**Use it when:** Describing a non-ohmic device (LED) at one spot on its curve, using two neighbouring data points.

**Example:** LED: 2.914 V @ 15 mA and 2.990 V @ 20 mA → Δr = 0.076 / 0.005 = 15 Ω.

### Percent error

```
error = (measured − nominal) / nominal × 100%
```

**Use it when:** Comparing your result with the part’s labelled value or a calculation. Keep the sign.

**Example:** Measured 1.08 Ω vs nominal 1 Ω → +8%.

### Tolerance range

```
Rnominal × (1 ± tolerance)
```

**Use it when:** Deciding if a part is within spec. Gold band = ±5%.

**Example:** 1 Ω ±5% → 0.95 Ω to 1.05 Ω.


## Report guide

1. Conductance = slope m of the resistor trendline, **in siemens**.
2. Resistance = 1/m.
3. % error vs nominal 1 Ω = (measured − nominal)/nominal × 100%.
4. Is 0.95 ≤ R ≤ 1.05 Ω? Name error sources (lead/clip/contact resistance, supply resolution, heating).
5. LED resistance from the whole-data trendline, and whether the LED obeys Ohm's law.
6. Δr at high current (two highest points).
7. Δr at low current (two lowest points). If ΔI reads 0, Δr is too large to measure here.

Attach both plots, export one PDF, upload to Brightspace, and sign out of the lab PC.

## Safety

- Resistors at high power get **hot**. Don't touch them while powered.
- Always set the **current limit before** raising the voltage.
- If you think you destroyed a part, throw it away so the next group doesn't get it.

---
*Made for ESE 123 students by a TA. The simulations use typical part values; your bench readings will differ by a few percent.*
