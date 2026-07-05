↩ [Return to Testing the Method Through Layered Reactivity](../../case-studies/testing-the-method-through-layered-reactivity.md)

# Twine Passage Rules

## Purpose

The production style guide behind the layered reactivity prototype — how passages, links, and system state stay readable and consistent while testing the three-layer system.

## Core Principle

Change one thing at a time; test after each change. Keep the player-facing hub simple and the debug/system view separate, so testing the mechanics never requires exposing them to the player.

## Explanation

The Vys hub (player-facing) shows city title, premise, mood, and movement links — never raw system values like pressure, trust, or faction score. Debug Vys (the control room) is allowed to show all of that: city state, pressure, layer influence, current action values, memories. The main hub should never look technical; debug should.

Links read as actions, not menu labels — `[[Enter Scutis Headquarters->Scutis Headquarters]]`, not `[[Scutis Headquarters]]`.

System state follows the same discipline as the layer logic itself: current action values are temporary and reset after each pressure application (`(set: $layer2CurrentValue to 0)`), while influence values are memory and should persist across the whole run. Debug output prefers plain language over raw variables — "Worker helped: yes/no" rather than printing a boolean directly — and consequence should read as atmosphere, not scoreboard: "Word in the streets: ..." rather than "Last visible change: ...".

Before changing layout or CSS, export a working backup — the same discipline as not touching CSS, structure, and logic all in one pass.
