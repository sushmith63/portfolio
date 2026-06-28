# Tap Memory Ring — design assessment (does it actually work?)

This is the engineering review that should have come *before* the pretty model.
It checks the mechanism against your real requirement, stress-tests it across
different taps, finds what the source docs (and my first model) glossed over, and
recommends a corrected design. Dated 2026-06-28.

---

## 0. Straight answer: did I assess, or improvise?

I **improvised a faithful illustration** of the concept written in your three
documents. I did not independently validate the mechanics first. Doing that now
surfaced one genuine make-or-break problem (Section 3) that the docs hand-wave and
my first 3D model actually got *wrong*. So: good catch — this needed doing.

---

## 1. Your requirement, restated (correct me if this is off)

- A **clip-on** ring around an existing **single-lever mixer** tap. No plumber, no
  tools, doesn't replace or permanently modify the tap.
- **Clamps a stationary part** of the tap and **fits many tap sizes**.
- User sets their **preferred lever position once**, by hand.
- Every time the lever returns to that exact spot, a **click / lock feel** signals it.
- v1 is **mechanical only** — it remembers the *position*, it does not measure
  temperature. Honest marketing: "find your spot again," not "perfect temperature."

If that's right, then the rest of this document is about *whether the proposed
mechanism can actually deliver it*, not whether the idea is good (it is).

---

## 2. How a single-lever mixer really moves (the basis for everything)

A single-lever mixer handle does **two** motions:
- **Tilt up/down** → controls **flow** (how much water).
- **Swivel left/right** about the vertical axis → controls the **hot/cold mix** =
  what you experience as **temperature**.

So your "saved spot" is, mechanically, **an angular position of the left/right
swivel**. The collar/body underneath is stationary; the handle swivels above it.

> Consequence: the device must detect/repeat **an angle of the swivel**, while the
> handle is *also* free to tilt up/down for flow. Hold that thought — it's why the
> naive design breaks.

---

## 3. The core problem the docs hide (and my model got wrong)

The build doc says: *"the device grips the collar and stays still, while a small
follower **tracks the lever** as it swivels."* That sentence quietly skips the
hardest question:

> **If the device body is clamped to the *stationary* collar, how does any part of
> it "follow" the *moving* lever — without being attached to the lever (which would
> break "clip-on, don't modify the tap")?**

You can't have it both ways with one rigid piece. A detent needs **two parts that
move relative to each other**: one tied to the stationary collar, one tied to the
moving swivel. My first model cheated by drawing the follower as part of the lever
pivot — i.e. it silently *attached to the handle*. That's not a clip-on device.

### The fix: a coupling element between the lever and an internal index ring

The device actually needs **three functional groups**, not the two the docs imply:

| Group | What it does | Moves with |
|---|---|---|
| **A — Clamp body** | grips the collar, holds everything still | stationary collar |
| **B — Index ring** | an internal ring that rotates as the handle swivels | the lever swivel |
| **C — Detent + lock** | spring-ball detent between A and B; an adjustable, lockable notch = the saved spot | sets the "memory" |

The missing piece is **how B is driven by the handle**. Best option:

- **A sliding fork / yoke** that lightly straddles the lever stem. When the handle
  **swivels** (temperature), it pushes the yoke around, rotating index ring B. When
  the handle **tilts** (flow), the yoke **slides vertically** in its guides, so flow
  changes don't disturb the temperature reading. This is the key invention: it
  separates the two motions, capturing only the swivel that matters.
- The spring-ball plunger (off-the-shelf) lives between B and A; the user-set,
  lockable notch is where it clicks. The user feels the click *through the handle*,
  because the handle drives B.

Alternative couplings, and why the yoke wins:
- *Friction collar around the rotating handle body* — works only on taps where a
  cylindrical part actually rotates with temperature; many arm-style levers don't.
- *Attach to the lever directly* — rejected: not clip-on.
- The yoke tolerates the widest variety of handle shapes, so it's the v1 pick, with
  a friction-collar variant as a possible second SKU.

**This single change is the difference between a device that works and a prop.**

---

## 4. Fit across sizes — the honest numbers

There are **two independent things that vary** between taps, and the design must
absorb both:

**(a) Collar diameter (the clamp).**
- Cartridges are fairly standard (35/40 mm dominate), but the *visible collar* that
  the device clamps is **not** — it varies in diameter and height by brand, and some
  bases are square, not round.
- A **pure soft liner** only absorbs a few mm of diameter by compression — realistically
  a single liner covers maybe a ~10–15 mm band before it's either too loose (won't
  hold, spot drifts) or too tight (won't fit / marks chrome).
- A **dial- or band-tightened mechanism** (BOA-style cable or worm band) covers a
  *much* wider diameter range; the soft liner then does the gentle gap-filling and
  anti-slip. This hybrid is the docs' recommendation and it's sound — but realistically
  you still need a **small adapter set (2–3 liner sizes)** for the extremes, and
  square/odd bases simply won't be covered by a round clamp.

**(b) Lever stem size/shape and height (the yoke).**
- Handles vary hugely (joystick, blade, teardrop, loop) and sit at different heights
  above the collar. The yoke jaws must be **compliant/padded and sprung** to grip a
  range of stem thicknesses, and the yoke's vertical travel must cover different
  tilt ranges.

**Realistic claim:** "fits **most common** single-lever mixers, possibly with a small
adapter kit" — **not** "fits every tap, zero install." Matching the docs, but now you
can see *why* from the mechanics.

---

## 5. Setting and re-setting the saved spot (an affordance the model is missing)

The memory only works if the user can **set** it easily:
1. Move the handle to your preferred warm spot.
2. **Lock** the notch to index ring B at that current angle (a thumb-turn or press).
3. Done — the ball now clicks there. To change seasons, unlock, move, re-lock.

My current model shows a fixed notch but **no setting/locking action**. A real design
needs that affordance (the tightening dial could double as the lock, or a separate
small slider). Worth showing, because "how do I save my spot?" is the first question
a user asks.

---

## 6. Failure modes & things you might not have considered

Thinking ahead for you (you said this is your first time — these are the traps):

- **Clamp slip = memory drift.** If the clamp body rotates even slightly on the
  collar, the saved angle moves with it. Needs **anti-rotation** (high-friction liner,
  or a feature that keys to a flat/notch on the collar).
- **Soft-liner creep.** Rubber/silicone relaxes over months and loosens — design for
  re-tightening (the dial helps).
- **The "collar rotates with the lever" tap.** The docs flag this: on some taps the
  whole collar turns, breaking the stationary-anchor assumption. Those need a variant
  that references the **fixed wall plate** instead — effectively a second product mode.
- **Flow vs temperature.** The yoke deliberately ignores flow-tilt. Decide: remember
  **temperature-swivel only** (recommended, simplest, matches the daily pain) or also
  remember flow? Some "joystick" levers couple the two diagonally — those are harder.
- **Clearance.** The housing must not block the handle's full swing, and the yoke must
  reach the stem — both vary with handle length/height.
- **Environment.** It lives at a wet sink: humidity, splashing, soap, cleaning. Materials
  and the click mechanism must tolerate that and stay hygienic.
- **Handedness / orientation.** Lever-on-top vs lever-on-side designs; left/right swing.

---

## 7. Does what I built match the requirement?

- **As a communication tool:** yes — it explains the concept and the parts clearly.
- **As an engineering design:** **partially.** It is missing (a) the coupling/yoke that
  makes "follow the moving lever" physically real, (b) the set/lock affordance, and (c)
  any depiction of size-adaptation. And it *mis-showed* the follower as part of the
  lever. So it's an honest illustration of the *story*, not yet a faithful model of a
  *working* device.

---

## 8. Recommended corrected design (consolidated)

- **Clamp (A):** soft liner **+ dial/BOA band** for wide range, **+ a 2–3 piece adapter
  set** for extremes; anti-rotation feature. Round bases only in v1.
- **Couple (B):** a **vertical-sliding yoke** on the lever stem → drives an internal
  **index ring**; captures swivel (temperature), ignores tilt (flow).
- **Memory (C):** **adjustable, lockable notch** + **off-the-shelf spring ball plunger**
  (force chosen for a crisp click; low backlash in the yoke for a clean feel).
- **Scope:** remember **temperature-swivel only** for v1; flow optional later.
- **Variants to plan for:** a wall-plate-referenced version for "rotating collar" taps;
  possibly a friction-collar coupling as a second SKU.

---

## 9. Decisions that are genuinely yours

1. **Memory scope:** temperature-swivel only (recommended) vs. temperature **and** flow?
2. **Fit strategy:** accept "most taps + small adapter kit," or chase wider universal fit
   (more cost/complexity)?
3. **Should I now revise the 3D model + notes** to show the corrected mechanism (yoke +
   index ring + set/lock), so the prototype tells the *true* working story?

---

## 10. What I'd do next (engineering-first order)

1. Lock the mechanism on paper (this document) — agree the yoke + index-ring architecture.
2. **Revise the interactive model** to show it truthfully (so it doubles as a design check).
3. Only then turn it into **parametric CAD** and print 1–2 samples.
4. Clip samples on several **real taps** — confirm the collar-stays-still assumption, the
   clamp range, and the yoke's grip on different handles. This physical test is the real
   judge and cannot be skipped.
