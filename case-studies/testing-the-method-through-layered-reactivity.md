# Testing the Method Through Layered Reactivity

*One of the applied methods behind this narrative design portfolio.*

## The Method

A reactive world should respond to the player without letting any single actor lose its shape.

The method is to separate actor identity from actor influence: a faction stays what it is, while how strongly its actions land depends on the current pressure inside the city it acts within.

## Explanation

A simple reputation bar — one faction up, another down, the world reacting through direct switches — makes every actor feel infinitely flexible. Identity starts to look like whatever the player last touched.

Separating identity from influence fixes this without adding unnecessary simulation. A faction remains itself; only the effectiveness of its actions shifts with context. Done right, this also prevents any single path from permanently dominating the city state — the stronger side can always be challenged, and the city keeps memory of how it got there.

## Application

Testing the method in Twine exposed four dependent design problems, each one created by solving the last.

### Avoiding Simple Reputation

Treating every action as a direct raise/lower on one faction produces a reactive but shallow world — the player moves numbers instead of changing pressure inside a living place.

The fix: treat each layer as a different scale of influence.

- **Layer 3 — NPC / Local Behavior:** individual NPCs, small groups, local trust, fear, access, personal consequences
- **Layer 2 — Faction Pressure:** organized groups, public authority, rebels, institutional force, coordinated action
- **Layer 1 — City / World State:** the wider condition created by accumulated pressure

Local behavior and faction pressure can now affect the city while keeping separate roles.

### Keeping Factions Stable

If player action could change a faction too easily, factions would stop feeling like institutions with memory, ideology, and limits. Scutis should remain Scutis. Novacula should remain Novacula — the city state can shift without rewriting what those factions are.

The fix: Layer 2 and Layer 3 influence each other's effectiveness while keeping separate identities. If Scutis currently has the upper hand, Novacula has a harder time regaining power through faction pressure alone — the player may need to build influence through NPCs and local reactions first before faction pressure becomes effective again. This creates an anti-snowball effect.

This same principle — identity stays fixed while effectiveness fluctuates with context — holds at the individual scale too. See Building NPCs Through Layered Pressure: an NPC's System Relationship (Believer, Rejector, Damaged Believer) doesn't change easily either, for the same structural reason a faction doesn't. Whether it can shift under sustained pressure is still an open question being tested — see the development diary's note on layer shifts as a test candidate, not yet confirmed as a working system.

### Making City State Reversible

A higher Scutis tier needs to be challengeable later; Novacula gaining ground still needs to leave room for order to return. The city needed to be stateful, but reversible.

The fix: city state changes through accumulated pressure, then reshapes future context. If the player lowers Scutis control through Novacula pressure, NPC influence recalculates through the new city context. No single path can permanently dominate the city state.

### Implementing the Loop in Twine

The prototype needed to test this logic without turning every passage into a full simulation.

The fix: quest passages only set the current layer values.

```twine
(set: $layer2CurrentValue to 4)
(set: $layer3CurrentValue to -2)
```

A pressure passage collects those values, applies them to city pressure, resets the temporary values, and moves the story into the city-state check:

```twine
(set: $pressureVysControl to $pressureVysControl + $layer2CurrentValue)
(set: $pressureVysControl to $pressureVysControl + $layer3CurrentValue)

(set: $layer2CurrentValue to 0)
(set: $layer3CurrentValue to 0)

(goto: "Layer 1")
```

Quest passages stay simple — they only report what kind of pressure they created. The pressure and city-state logic handle the wider consequence. The full production discipline behind this — hub vs. debug view, link phrasing, state reset rules — is documented in [Twine Passage Rules](../vault/case-study-03/twine-passage-rules.md), part of Noeme Systems.

## Result

The final loop:

```text
NPC action → Layer 3
Faction action → Layer 2
Layer 2 and Layer 3 modify each other's effectiveness
Layer 2 + Layer 3 → Pressure
Pressure → Layer 1 City State
Layer 1 City State → future NPC behavior, faction access, location mood, and quest logic
```

This connects back to the wider portfolio method chain: past experience + current situation → emotional state → reason → behavior → new experience. In the prototype, experiences create pressure; influence decides how far that pressure spreads; layers decide where it acts.

Together with the previous two case studies, this shows the same method holding across scales: history creating pressure, the chain scaling from character to institution, and now that logic tested inside an interactive prototype — pressure that moves values instead of resetting them.

## Evidence

- [Layer Test Twine Prototype →](https://vedirago.github.io/diogo-oliveira-portfolio/Layer%20Test%20Twine/index.html)
- [Twine Passage Rules — Noeme Systems](../vault/case-study-03/twine-passage-rules.md)
- Building NPCs Through Layered Pressure

---

← Previous: [Building a Modular Narrative Method](./building-a-modular-narrative-method.md) · [README](../README.md) · Next: Building NPCs Through Layered Pressure →