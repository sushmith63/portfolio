# How this problem is already solved — and the best way to build our version

In-depth research into how existing products solve "remember a rotary shower
handle's position," what the real gap is, and the honest best mechanism — including
a direct answer to "two rings both on the collar, how do you keep one still?"
Dated 2026-06-28.

---

## 1. It's already solved *inside* the tap: the Rotational Limit Stop (RLS)

Every modern single-handle pressure-balance shower valve (Delta, Moen, Gerber,
Kohler…) already has a settable angular memory built in — the **Rotational Limit
Stop**, an anti-scald part:

- It's a **white/grey toothed plastic ring** that sits **on top of the cartridge,
  under the handle** — *between the fixed cartridge/bonnet and the rotating stem*.
- You **set it once** (pull it up off the splines, rotate, push back); each tooth
  ≈ 4–6 °F. It then **physically limits** how far the handle rotates toward hot.

**Why this matters enormously for us — three takeaways:**
1. The mechanism we want (a *settable angular detent on a rotary valve*) is **proven,
   cheap, reliable, and already mass-produced**. Low technical risk.
2. It tells us **where a fixed reference actually lives**: the **cartridge/bonnet
   directly under the handle** is stationary — not just the escutcheon plate.
3. Its limits: it's a **hot-*limit* (a hard stop), not a *click at your favourite
   spot*; it's **built-in, not retrofit**; and you must **pull the handle** to set it.

**Our product = an external, retrofit, *adjustable, clicky* version of the RLS that
clicks at your saved spot instead of just capping the top.** That's the honest
one-line definition, and the RLS proves it's buildable.

## 2. The market gap is real (confirmed)

Searching aftermarket/retrofit options turns up only: built-in memory valves
(Kohler Rite-Temp, Moen — premium, installed), digital/smart showers (expensive,
in-wall), temperature-display showerheads, and replacement handles. **No one sells
an external clip-on that clicks at your saved spot.** The gap the earlier docs
claimed is confirmed by search.

## 3. The core engineering question: where is the "still" part?

A detent needs **two parts that move relative to each other** — one fixed, one
moving. On your tap the handle **and** the collar rotate, so the only question that
matters is: *what do we use as the fixed reference?* There are exactly three honest
candidates, and this — not the ring shape — is the real design decision.

| Option | The "still" reference | Install | Fits many taps? | Reliability | Notes |
|---|---|---|---|---|---|
| **A. Plate-edge clip** | escutcheon wall plate | none | **poor** — plates vary the most (square/round, many sizes) | medium | your current pick; awkward to grip a flat plate |
| **B. Behind-the-handle ring** | cartridge/bonnet (where the RLS already references) | ~5 min, one set screw | **good** — cartridges are far more standard (35/40 mm) than plates | **high** | basically an external, clicky, easy-to-adjust RLS |
| **C. Gravity ring on the collar** | **gravity** (a weighted free ring) | **none** (clips on the collar) | good for wall valves | medium (bearing friction) | answers your two-ring idea; novel; horizontal-axis only |

**Honest note on your chosen Option A:** clipping the plate edges is genuinely
*no-install*, but the plate is the **least standardised part of the whole tap**, so
it's actually the **worst** choice for "fits many taps," and gripping a smooth flat
plate firmly enough that the saved spot doesn't drift is awkward. It works, but it
fights the universality goal you care about.

## 4. Your idea, solved: "two rings on the collar — how do you keep one still?"

You're right that we can put two rings on the collar — but if **both** clamp the
collar, they **both rotate together**, so there's no relative motion and no click.
The trick to make one "still" without bolting it to anything is **gravity**:

- **Ring 1 (the reference):** spins **freely** on the collar (on a low-friction
  bearing) and has a **weight at the bottom**. Gravity keeps the weight hanging
  down, so this ring **stays vertical — it does not turn with the collar.** That's
  your "still" part, created out of thin air.
- **Ring 2 (the driver):** **clamps** the collar, so it turns with the handle.
- **Detent** (spring ball on Ring 2, adjustable notch on Ring 1) clicks when the
  handle returns to your saved angle. Your spot is stored as **an angle from
  vertical**, which is constant for that tap.

This is elegant: **truly no-install** (just clip onto the collar), it **doesn't
care** whether the collar rotates, and it's **potentially novel** (good for a
patent). 

**Honest risks of the gravity method (must prototype these):**
- **Bearing friction vs. the weight.** If the bearing drags, Ring 1 creeps when the
  collar spins → the saved spot drifts. The weight must reliably overcome bearing
  friction *and* the sideways push of the ball-detent at the click. This is the make-
  or-break test.
- **Only works on a horizontal axis** (wall shower valves — like yours). On a
  deck/kitchen mixer the temperature axis is vertical, so gravity gives no
  reference there.
- Knocks/vibration swing the pendulum briefly (it re-settles).

## 5. The honest truth about "one device for all taps"

There is **no single device that fits every tap**, because tap types move
differently:
- **Wall rotary shower valves** (yours): handle rotates about a *horizontal* axis →
  Options B and C both work well.
- **Deck single-lever mixers** (kitchen/basin): temperature is a *swivel about a
  vertical* axis → gravity (C) fails; you'd reference the deck/plate or the body.

So the right strategy is **segment by tap type and pick a beachhead**. Your actual
pain is the **cold shower** → the **wall shower valve** is the market to win first,
and it's exactly where Options B and C shine. Chasing "every tap on earth with one
part" is the trap the docs warned about.

## 6. Recommendation

1. **Reframe the product honestly:** an external, retrofit, adjustable, *clicky*
   Rotational Limit Stop for single-handle shower valves. (Proven mechanism, real gap.)
2. **Prototype two reference strategies side by side** — they're cheap to print:
   - **Option B (behind-the-handle ring)** as the *reliable baseline* — most robust,
     most universal across cartridges, ~5-min install.
   - **Option C (gravity ring on the collar)** as the *exciting no-install bet* —
     test whether a weight can reliably beat bearing + detent friction. If it can,
     it's the better product and possibly patentable.
3. **Treat Option A (plate-edge clip) as a fallback**, not the lead — it's the
   weakest for the fits-many-taps goal you care about.
4. Focus on **wall shower valves first** (matches your tap and the cold-shower pain).

**Sources**
- Delta — set the adjustable rotational limit stop: https://support.deltafaucet.com/s/article/How-do-I-set-the-adjustable-rotational-limit-stop-on-my-bath-or-shower-1628028366789
- PHCP Pros — shower limit-stops explained: https://www.phcppros.com/articles/10227-shower-limit-stops
- Engineer Fix — adjust an anti-scald / scald-guard valve: https://engineerfix.com/how-to-adjust-a-delta-scald-guard-for-maximum-temperature/
- Gerber — single-handle shower temp-limit device adjustment: https://support.gerber-us.com/hc/en-us/articles/34836549456155
- Built-in memory comparison (Kohler Rite-Temp / Moen / Delta TempAssure): https://www.deltafaucet.com/design-innovation/innovations/shower/tempassure-valve--monitor-valve
- Shower temperature display patent (prior art, electronic route): https://patents.google.com/patent/US7124452B1/en
