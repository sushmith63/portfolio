# Tap Memory Ring — working notes (research + AI capability)

Companion to `tap-memory-ring-prototype.html`. This file is the running "saved
memory" for the project: what the prototype shows, fresh research on the two
open questions, and an honest read on how far an AI can actually take this from
idea to product. Dated 2026-06-28.

---

## 1. What the interactive prototype now shows

Open `tap-memory-ring-prototype.html` in a browser. It is a single self-contained
file (3D via Three.js from a CDN). Buttons across the bottom:

- **Overview** — the whole device clipped on a tap, every part labelled with the
  doc's codes (T1–T4 = tap parts, P1–P5 = our device parts). Toggle **Legend**
  for the glossary, **Labels** to hide/show callouts.
- **How it grips** — turn the dial (P3) and the soft liner (P2) squeezes inward
  and clamps onto the collar (T2). Inward arrows show the clamping direction.
- **How it clicks** — the lever (T3) swivels; the spring-loaded follower ball
  (P5) rides the detent track and drops into your saved-spot notch (P4). The
  notch glows and a **"click!"** pops at the moment it seats.
- **Take apart** — every part separates along the axis so you can see them one
  by one.
- **Product story** — the business summary (idea, the five grip options,
  cost & roadmap, naming) pulled from the three source documents.

Each mode moves the camera to frame *its own* mechanism and shows only the
labels relevant to that mode, so the moving parts are easy to follow.

> This is an **illustrative / communication** model — correct in how the
> mechanism behaves, not a manufacturing CAD file. See section 3 for the
> difference and how to cross that gap.

---

## 2. The two open questions — fresh research

### 2a. The temperature question: is there public data / an API for a home's hot & cold water temps?

Short answer: **there is no single "household water temperature" API, but the
*cold* side can be estimated from public data, and the *hot* side cannot —
which is exactly why position-memory (not temperature) is the right v1.**

**Cold (incoming mains) water — estimable from public data.**
- Incoming mains temperature is well-documented by region and season. It ranges
  from roughly **40 °F (≈4 °C) in the far north to ~80 °F (≈27 °C) in the south**,
  and swings with the seasons. Free city/ZIP-level maps exist (Bradley, Rinnai,
  HydroFLOW) that the tankless-water-heater industry already uses for sizing.
- There is a published model — the **Christensen–Burch correlation**, used in the
  DOE's EnergyPlus engine — that estimates daily mains temperature from the local
  ground temperature and a 31-day running average of outdoor air temperature
  (`T_inlet = T_ground × 0.65 + T_avg31 × 0.35`). Outdoor temperature *is*
  available from weather APIs (e.g. NOAA), so you could approximate a home's cold
  inlet temperature for a given location and date. That's the closest thing to an
  "API" for this.

**Hot water — not publicly knowable per home.**
- Hot supply is a *setpoint on each home's heater*, not published data. The
  common default is **120 °F (≈49 °C)** (CDC recommends ≤120 °F; many units ship
  lower). But the dial setting doesn't even guarantee the outlet temperature —
  pipe heat-loss and each household's heater differ.

**What this means for the product (confirms the docs, now with sources):**
- You could *estimate* the cold side by location + season from public/weather
  data, but the hot side is unknown per home and the lever-position→temperature
  mapping differs per tap. So a pure-maths "guess the temperature" feature would
  be unreliable and is rightly **out of scope for v1**.
- Honest framing stays: the device **remembers your spot**, it doesn't measure
  degrees. If temperature feedback is ever wanted, sense it *at the water*
  (cheap thermochromic strip or a water-powered colour showerhead), not by
  calculating it on the dry collar.

### 2b. The "click" part is off-the-shelf — concrete components exist

The detent (the click) does not need to be invented. **Spring-loaded ball
plungers / ball detents** are a standard catalogue part:
- Standard metric threads **M3, M4, M5, M6, M8, M10, M12**; ball diameters
  ~1.5–6 mm; bodies ~6–25 mm long.
- Selectable spring force — roughly **1.2 N to 15 N initial, up to ~30 N**, in
  "standard" and "heavy" loads, so the click feel is a spec you choose.
- Suppliers with same/next-day delivery: **McMaster-Carr, Carr Lane, Halder**,
  plus low-cost packs on Amazon for prototyping.

So for the build, P5's ball is an off-the-shelf plunger; only the **track + notch
(P4)** it rides in is a custom moulded/printed part. That keeps cost and risk down.

**Sources**
- Cold inlet / groundwater temp data: [Bradley Corp — US groundwater temperatures](https://www.bradleycorp.com/sizing-tankless-water-heaters/united-states-groundwater-temperatures), [Rinnai ground water temp map (PDF)](https://www.rinnai.us/download/download?path=%2Fs--3Vzm5qS_--%2Fe54fa7f3039734fadb199f805ee01d527e4aee37.pdf&filename=North+America+Ground+WaterTemp+Map.pdf), [Tank The Tank — incoming water temp map](https://tankthetank.com/pages/average-incoming-water-temperature-map-of-the-united-states)
- Mains-temp model: [EnergyCodeAce — Cold Water Inlet Temperature](https://energycodeace.com/site/custom/public/reference-ace-2016/Documents/52b42coldwaterinlettemperature.htm), [Unmet Hours — cold inlet water temperature](https://unmethours.com/question/9568/how-to-get-the-cold-inlet-water-temperature/)
- Hot setpoint: [US DOE — lower water heating temperature](https://www.energy.gov/energysaver/do-it-yourself-savings-project-lower-water-heating-temperature), [PHCP Pros — hot water system temperatures and the code](https://www.phcppros.com/articles/1828-hot-water-system-temperatures-and-the-code)
- Detent components: [McMaster-Carr — ball detents](https://www.mcmaster.com/products/ball-detents/), [Carr Lane — ball plungers](https://www.carrlane.com/product/spring-loaded-devices/ball-plungers), [Halder — spring plungers with ball](https://www.halderusa.com/PM/Standard-Parts/Machine-and-Fixture-Elements/Spring-Plungers/Spring-Plungers-with-ball-and-internal-hexagon)

---

## 3. How far can AI actually take this — honest answer

You asked the big question repeatedly: *can an AI take my inputs and design,
assess, and develop this front-to-back?* Here is the straight version.

### What AI does genuinely well here (and has already done)
- **Research & synthesis** — market size, prior art/patents, tap standards,
  materials, cost ranges, patent routes. (Your three documents.)
- **Documentation, naming, go-to-market copy.**
- **Illustrative interactive prototypes** — like the 3D file here — to explain
  the mechanism and make figures. Great for communicating and pitching.
- **Parametric CAD *via code*** — tools like **OpenSCAD, CadQuery, build123d**
  let an AI write a script that outputs a *real* `STL`/`STEP` file you can send
  to a printing service. This is the bridge from "picture of the idea" to "part
  you can hold." (Offered as the next step below.)
- **Any software/firmware** if a later version adds electronics or an app.

### What AI cannot do — the physical and accountability gap
- **Print it and test fit + click on many real taps.** This is the single
  riskiest assumption in the whole project (one ring, many collar sizes) and it
  is hands-on. No AI can do it. It cannot be skipped or simulated away.
- **Sign off that a part is manufacturable** — draft angles, wall thickness,
  undercuts, tolerances, mould design. An engineer must own this.
- **Validate real demand** — AI can draft the survey and landing page; it can't
  be the 20–30 real people who say "I'd pay for this."
- **File a *strong* patent, handle certification, tooling, suppliers.** AI can
  draft a cheap provisional, but a thin one is weak; real value needs an attorney.

### The realistic AI-assisted pipeline
1. Research, concept, documents — **AI (done).**
2. Communicative interactive prototype — **AI (done — this file).**
3. Parametric CAD → printable `STL`/`STEP` — **AI-assisted, engineer-reviewed.**
4. **3D-print and test fit + click on real taps — human. Non-negotiable.**
5. Iterate the design from what fails — AI helps redesign fast.
6. DFM + costing + provisional-patent draft — AI-assisted, human/attorney review.
7. Soft tooling, pilot run, certification, launch — human + manufacturer.

### The honest bottom line
The **maximum** you can get *from AI* is everything up to the physical world: a
fully-researched concept, a clear interactive prototype, **printable parametric
CAD**, and all the supporting docs/marketing. AI is a force-multiplier on
research, design drafting, software and communication — but the value still turns
on the cheap physical steps it *can't* do for you: print a few, clip them on real
taps, and confirm people will pay. Do those before spending on tooling.

---

## 4. Status & what's pending

**Done**
- Reviewed all source material; rebuilt the broken 3D prototype with correct,
  legible grip/click/take-apart mechanics and a product-story panel.
- Researched the temperature-data and detent-component questions (section 2).

**Open decisions (yours)**
- Grip: soft liner + dial (recommended) vs. worm-drive band.
- Anchor: pure clip-on (collar) vs. 5-minute stem-anchored fit (more repeatable).
- Temperature: leave out of v1 (recommended) vs. bundle a cheap colour showerhead later.
- First target market/region.

**Suggested next steps (cheapest, highest-value first)**
1. Generate **parametric CAD** (code → real STL) and order one or two
   3D-printed samples from an online service (~tens of dollars).
2. Clip the samples on several real taps — confirm the collar-stays-still
   assumption and the fit range.
3. Talk to 20–30 people who have this annoyance; would they pay $20–40?
4. Once the design is real, file a low-cost provisional patent.
