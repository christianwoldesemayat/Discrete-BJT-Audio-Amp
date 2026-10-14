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
