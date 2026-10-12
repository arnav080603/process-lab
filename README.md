# ⚗️ Process Lab: interactive chemical engineering simulators

**▶ Try it live: https://arnav080603.github.io/process-lab/**

Five browser-based simulators covering core topics from a chemical engineering degree, from reaction engineering to process control. Each one is built from first principles and has its equations written out, so you can see *why* the numbers come out the way they do.

![Distillation module](screenshots/distill.png)

## Modules

| Module | What you can do | Engineering behind it |
|---|---|---|
| **⚗️ Reactors** | Compare a CSTR and a PFR, change temperature, volume, flow and reaction order, and find the volume needed for a target conversion | Arrhenius kinetics, design equations for ideal reactors, Damköhler number |
| **🧪 Distillation** | Design a binary column graphically: watch the McCabe–Thiele staircase, minimum reflux pinch and feed-stage location update live | VLE with constant relative volatility, q-line, R<sub>min</sub>, Fenske equation, Gilliland correlation |
| **🎛️ Process Control** | Tune a PID level controller on an animated P&amp;ID, step the setpoint, open a drain valve, switch to manual | Dynamic tank mass balance with dead time, PID with anti-windup and bumpless transfer, offset vs. integral action, instability |
| **🔥 Heat Exchanger** | Size a double-pipe exchanger and flip between counter- and co-current flow | ε-NTU method, LMTD, energy balances, temperature cross |
| **📓 Lab Notebook** | Enter your own experiment data and fit an activation energy | Linearized Arrhenius regression, R², extrapolation |

## Screenshots

| Reactors | Process control |
|---|---|
| ![](screenshots/reactor.png) | ![](screenshots/control.png) |
| **Heat exchanger** | **Lab notebook** |
| ![](screenshots/hx.png) | ![](screenshots/kinetics.png) |

## Validation

I checked the models against textbook answers:
- **Distillation**, α = 2.5, x<sub>F</sub> = 0.5, x<sub>D</sub> = 0.95, x<sub>B</sub> = 0.05, saturated-liquid feed: R<sub>min</sub> = 1.10 and N<sub>min</sub> = 6.43 (both match the hand calculation). At R = 1.5 R<sub>min</sub>, the staircase gives 12 stages, while the Gilliland correlation estimates 12.3.
- **Reactors:** first order with Da = 10 gives X<sub>CSTR</sub> = 0.909 and X<sub>PFR</sub> = 0.99995. For second order, the CSTR solution satisfies Da(1−X)² = X exactly. Required-volume formulas round-trip back to the target conversion.
- **Heat exchanger:** Q from ε-NTU equals U·A·ΔT<sub>lm</sub> and both streams' energy balances to machine precision. With C<sub>r</sub> = 1 and NTU = 1, ε = 0.5 as expected.
- **Process control:** the "well tuned" preset settles a 0.8 m setpoint step in about 34 s with 3% overshoot and rejects a drain-valve disturbance. The "aggressive" preset oscillates indefinitely, and P-only control leaves a steady-state offset, as theory predicts.

## The real experiment
The Lab Notebook pairs with a kitchen-safe experiment: time how long an effervescent tablet takes to dissolve at different water temperatures, then fit an Arrhenius plot to estimate an activation energy. The prefilled numbers are clearly labelled example data.

## Tech
A single `index.html`: vanilla JavaScript with hand-written Canvas charts and animations (no charting library), and KaTeX for the equations. No build step, no backend. To run it locally, open the file or run `python3 -m http.server`.

*Built by Arnav Sharma with help from AI coding tools (Claude Code). I chose the topics, checked the results against textbook methods, and plan to study chemical engineering.*
