# 4-Stage Common-Emitter Amplifier: Design, Simulation & PCB (LTspice + KiCad)

An end-to-end analog audio amplifier project, taken from first-principles math all the way to a manufacturable board, using LTspice and KiCad.

**What's inside:**
- Theoretical analysis and hand calculations for each stage
- LTspice simulations and results
- Breadboard prototype with real-world measurements
- Final PCB design in KiCad

## Step 1: Designing the Common-Emitter Input Stage

**Objective:** Design the amplifier's first gain stage using a common-emitter configuration to provide high voltage gain.

**Details:** This phase sets a stable DC operating point, then uses AC small-signal analysis to set the gain and calculate the lower and upper cutoff frequencies that give the stage its band-pass response. The design assumes a transistor current gain of $\beta = 180$ and runs from a ±15 V dual supply. It targets:

- Voltage gain: $|A_v| \geq 30$
- Output swing: 22–24 V peak-to-peak
- Bandwidth covering the full audio range: $f_L \leq 20\ \text{Hz}$ and $f_H \geq 20\ \text{kHz}$

The design is verified in LTspice with operating-point (`.op`), frequency-response (`.ac`), and transient (`.tran`) simulations.

<img width="923" height="908" alt="faz1" src="https://github.com/user-attachments/assets/33a52db3-6648-44ee-b5ce-4e33b8b42c40" />


## Step 2: Emitter-Follower Buffer & Multistage Cascade

**Objective:** Add an emitter-follower (EF) buffer stage and expand the design into a multistage cascaded amplifier, preventing loading effects from degrading the gain.

**Details:** To reach a higher overall gain, two common-emitter stages are cascaded and followed by an emitter-follower stage. The follower provides a high input impedance and a low output impedance, so the gain stages aren't loaded down by what comes after them. Inter-stage coupling capacitors are chosen carefully so the cascaded system still covers the full 20 Hz – 20 kHz audio band. The multistage design targets:

- Total voltage gain: $|A_v| \geq 200$
- Maximum output swing: greater than 20 V peak-to-peak
- Power dissipation: below 0.2 W in every resistor

<img width="1341" height="910" alt="faz2B" src="https://github.com/user-attachments/assets/04f73a99-a61b-49e4-ba52-b9cf1265c24a" />
<img width="954" height="913" alt="faz2A" src="https://github.com/user-attachments/assets/7073c689-6c4b-4a7b-b03b-6bf64ab06ffc" />

## Step 3: Class AB Output Stage, Component Selection & Full Integration

**Objective:** Design a Class AB push-pull output stage that can drive an 8 Ω speaker, replace the ideal SPICE transistor models with real commercial BJTs, and complete the four-stage amplifier.

**Details:** The final amplifier has four stages: two common-emitter gain stages, an emitter-follower buffer, and a Class AB power output stage. Moving from ideal models to physical components required detailed datasheet analysis, choosing each transistor for its thermal stability, current capability, and transition frequency ($f_T$). The output stage uses a complementary push-pull pair with diode biasing, which keeps both transistors slightly on to minimize crossover distortion. The complete system targets:

- Total voltage gain: $|A_v| > 1000$
- Output power: $\geq 2\ \text{W}$ into an 8 Ω load
- Total power consumption: below 10 W

**Components selected:**

| Stage | Part | Reason |
|---|---|---|
| Input & intermediate gain (CE) | `BC546B` | High $V_{CEO}$ breakdown voltage and consistent current gain |
| Driver / buffer (EF) | `BD139-16` | Thermal stability and medium-power handling |
| Power output (Class AB push-pull) | `BD139` (NPN) & `BD140` (PNP) | Complementary pair for symmetrical push-pull operation |
| Bias network | `1N4148` | Forward voltage sets the output pair's quiescent bias |

## Step 4: Breadboard Prototyping, Measurement & PCB Design

**Objective:** Validate the calculated and simulated design with real hardware, then turn the proven circuit into a printed circuit board (PCB).

**Details:** The complete amplifier is first built on a breadboard to see how it performs with real-world parasitics, thermal drift, and component tolerances. DC offset, voltage gain, output power, and frequency response are measured with an oscilloscope and multimeter. Once the prototype meets its targets, a two-layer PCB is laid out in KiCad. The layout follows these design rules:

- Minimum trace width: 1 mm for power lines and 0.3 mm for signal lines
- Dedicated copper areas for heat sinking the power transistors
- Design Rule Check (DRC) passed with zero errors
