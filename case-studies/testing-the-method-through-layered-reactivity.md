# Case Study 03 — Testing The Method Through Layered Reactivity

## Main Problem

After building the world logic and [modular method](building-a-modular-narrative-method.md), the next question was whether the same thinking could drive a reactive prototype.

I did not want a simple reputation bar where one faction goes up, another goes down, and the world reacts through direct switches. That kind of system can make factions feel too flexible, as if their identity changes whenever the player touches them.

The challenge was to let the world react without making every actor lose its shape.

A faction should remain itself. A local character should remain local. A city state should change, but not erase the identity of the forces acting inside it.

## Main Solution

I tested the method in Twine through a layered reactivity system.

The solution was to separate actor identity from actor influence.

A local action does not become a faction action just because it affects the city. A faction action does not become a local action just because citizens react to it. Each layer keeps its role, while still influencing the effectiveness of the others.

The working structure became:

```text
Layer 3 — NPC / Local Behavior
Layer 2 — Faction Pressure
Layer 1 — City / World State
```

The key rule was:

```text
Actor decides layer.
Pressure decides city.
City decides future context.
```

## Problem 01 — Avoiding Simple Reputation

The first risk was turning the system into a disguised reputation meter.

If every action simply raised one faction and lowered another, the world would feel reactive but shallow. The player would be moving numbers, not changing pressure inside a living place.

## Solution

I treated each layer as a different scale of influence.

Layer 3 handles local behavior: individual NPCs, small groups, local trust, fear, access, and personal consequences.

Layer 2 handles faction pressure: organized groups, public authority, rebels, institutional force, and coordinated action.

Layer 1 handles the city or world state: the wider condition created by accumulated pressure.

This allowed local behavior and faction pressure to affect the city without becoming the same thing.

## Problem 02 — Keeping Factions Stable

The second problem was faction identity.

If player action could change a faction too easily, factions would stop feeling like institutions with memory, ideology, and limits.

Scutis should not become Novacula just because the player pushes the city in a different direction. Novacula should not become Scutis because the city temporarily favors order.

## Solution

Layer 2 and Layer 3 influence each other's effectiveness, but not each other's identity.

A faction remains itself. What changes is how strongly its actions land inside the current social condition of the city.

If Scutis currently has the upper hand, Novacula has a harder time regaining power through faction pressure alone. The player may need to work through local behavior first, building influence through NPCs and smaller social reactions before faction pressure becomes effective again.

This creates an anti-snowball effect.

The stronger side can be challenged, but not by pretending the city has no memory.

## Problem 03 — Making City State Reversible

The city could not end in only one fixed state.

If Scutis reached a higher tier, that should not permanently freeze the city. If Novacula gained ground, that should not permanently erase the possibility of order returning.

The city needed to be stateful, but reversible.

## Solution

The city state changes through accumulated pressure, then reshapes future context.

A change in city state can reset or reframe local influence because the social environment has changed. If the player lowers Scutis control from one tier to another through Novacula pressure, NPC influence is recalculated through the new city context.

This means the system allows change through local behavior, faction pressure, or both, while preventing any single path from permanently dominating the city state.

## Problem 04 — Implementing The Loop In Twine

The next challenge was implementation.

The prototype needed to test the logic without turning every passage into a complex simulation.

## Solution

Quest passages only set the current layer values.

```twine
(set: $layer2CurrentValue to 4)
(set: $layer3CurrentValue to -2)
```

A pressure passage then collects those values, applies them to the city pressure, resets the temporary values, and moves the story into the city-state check.

```twine
(set: $pressureVysControl to $pressureVysControl + $layer2CurrentValue)
(set: $pressureVysControl to $pressureVysControl + $layer3CurrentValue)

(set: $layer2CurrentValue to 0)
(set: $layer3CurrentValue to 0)

(goto: "Layer 1")
```

This keeps the quest passages simple.

They do not need to know the entire city system. They only report what kind of pressure they created. The pressure and city-state logic handle the wider consequence.

## Result

The prototype showed that layered reactivity can remain fluid without becoming shapeless.

Local behavior, faction pressure, and city state can affect one another without collapsing into one system.

The method also kept the design scalable. New quests do not need to rewrite the whole structure. They only need to decide what layer they affect and how strongly.

The final loop is:

```text
NPC action -> Layer 3
Faction action -> Layer 2

Layer 2 and Layer 3 modify each other's effectiveness

Layer 2 + Layer 3 -> Pressure

Pressure -> Layer 1 City State

Layer 1 City State -> future NPC behavior, faction access, location mood, and quest logic
```

This connects back to the wider portfolio [method chain](../vault/case-study-02/method-chain.md):

```text
past experience
+
current situation
-> emotional state
-> reason
-> behavior
-> new experience
```

In the prototype, experiences create pressure. Influence decides how far that pressure spreads. Layers decide where that pressure acts.

## What This Proves

This case study tested whether the earlier worldbuilding method could become playable structure.

[Case Study 01](building-a-world-to-test-quest-design.md) showed how history can create pressure.

[Case Study 02](building-a-modular-narrative-method.md) showed how the method can scale from character to place, history, and quest logic.

Case Study 03 tested that logic inside an interactive prototype.

The result is a reactivity model where choices do not only change numbers. They change context.

---
© Diogo Oliveira — June 2026
