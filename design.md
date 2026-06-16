# Cooperative Expedition Simulator

*A game about maintaining a shared mental model of a complex system under uncertainty.*

## Purpose

This document describes a game design exploration.

The goal is not to define a complete game, but to investigate a style of cooperative gameplay centered around collaborative sense-making, uncertainty, and crew resource management. Many mechanics, implementation details, and setting elements remain intentionally open.

The document should be read as a design thesis rather than a detailed specification.

## Problem statement

Most co-op games do not really invoke the spirit of coordination and cooperation, and true cooperative satisfaction is missing. Why is that? Co-op games fall into several categories:
- Co-op campaigns: Several people do something together, which could also be done alone
- Role-based co-op: Each player has a unique role, which cannot dynamically be swapped, either due to artificial skills or information asymmetry.
- Load-based co-op: No player is special, but there is too much to do for one player alone
In all these, either roles become repetitive and specialists become isolated, or one player becomes a planner and the others are just executing, or everyone plays "next to" each other instead of together.

Observation: real-world teams do not cooperate because of role restrictions. They cooperate because:
- Systems are complex.
- Information is incomplete.
- Time is limited.
- Attention is limited.
- No individual can understand everything.
Examples include aircraft crews, ship crews, mission control teams etc. In these environments:
- Everybody sees part of reality.
- Nobody sees all of reality.
- Maintaining a shared understanding becomes a task in itself.

## Core Design Goal

Create a game in which cooperation emerges naturally. Players should cooperate because it is useful, not because the rules force them to.
The game should reward:
- Communication
- Cross-checking
- Hypothesis generation
- Shared planning
- Situational awareness
- Risk management
We propose to build a game where maintaining an accurate and complementary model of (game) reality is success-critical.

## Core Principle

**The game is about maintaining an accurate model of reality.** The vessel, the world, the navigation system, and the engineering systems merely provide the context in which this activity takes place.

Failure occurs when:
- Reality changes.
- The crew's understanding does not.

Success occurs when:
- The crew continuously updates its shared understanding.
- Plans are adapted to changing conditions.

What the game is not:
- Not a realistic spacecraft simulator.
- Not a combat-focused game.
- Not a class-based RPG.
- Not a factory-building game.
- Not a game about twitch reflexes.

## Design cornerstones

#### 1. Emergent Specialization
- Every player can access every system.
- No artificial class restrictions.
- Specialization emerges from:
  - Familiarity
  - Context
  - Workload
  - Expertise
#### 2. Shared Operational Picture
- Players work from shared maps.
- Shared notes.
- Shared plans.
- Shared objectives.
- The operational picture is continuously updated.
#### 3. Reality is hidden and only indirectly revealed
- Systems report observations and do not reveal root causes
- Measurements may be incomplete or inaccurate.
- Players must investigate and form hypotheses.
- Plans are based on estimates rather than certainty.
- Verification is an ongoing activity.
#### 4. Expeditions, Not Battles
- Travel is the primary activity.
- Exploration is the primary purpose.
- [Maybe] Combat is an occasional disruption.
#### 5. Consequences Matter
- Resources are limited.
- Damage persists.
- Mistakes create future problems.
- Success creates future opportunities.

## Example

The crew notices fuel consumption exceeds prediction.
Possible explanations:
- Navigation error
- Fuel leak
- Sensor failure
- Engine inefficiency
- Environmental conditions

No player immediately knows the answer, so investigation becomes a collaborative activity and the gameplay emerges from the process of understanding.

## Success Criterion

The desired player conversation is:
- "That explanation does not fit the evidence."
- "Can somebody verify this?"
- "What are we missing?"
- "Let's revisit our assumptions."
The desired player experience is:
- We figured it out together.
- We adapted.
- We made it home.

## Why existing games don't quite do this

Many existing cooperative games contain elements of the desired experience, but none place maintaining a shared mental model at the center of gameplay.

### Typical shortcomings

- Information is too complete.
  - The game directly reveals the state of the world.
  - Players diagnose symptoms by reading UI elements rather than investigating.
- Roles are artificially restricted.
  - Cooperation is enforced by game rules rather than emerging from complexity.
- Tasks become repetitive.
  - Specialists often execute routines instead of solving new problems.
- Combat dominates.
  - Exploration, logistics and planning become secondary to fighting.

### Examples

#### 1. Artemis
- Captures multi-station ship operation.
- Stations are largely independent and information is mostly reliable.
#### 2. Barotrauma
- Strong engineering and damage-control gameplay.
- Focuses on immediate crises rather than long-term expedition planning.
#### 3. Stormworks
- Excellent vehicle and systems simulation.
- Focuses on building and operating machines rather than collaborative diagnosis and decision-making.
#### 4. Space Station 13 / 14
- Rich emergent interactions.
- Social simulation tends to dominate operational simulation.
#### 5. Factorio
- Strong systems thinking and logistics.
- Cooperation is often parallelized rather than requiring a shared understanding.

### Goal

Borrow the best ideas from these games:
  - Multi-station operation
  - Resource management
  - Damage control
  - Emergent problem solving

While placing the primary focus on:
    - Shared situational awareness
    - Collaborative diagnosis
    - Planning under uncertainty
    - Crew resource management

## Game outline

The game takes place in a fictional world on board a vessel. The goal of the game is to explore the world, by harvesting resources from the world and using them to keep the vessel operating and improve it.

The setting exists primarily to support the gameplay. The exact nature of the world is intentionally left open. For the sake of this discussion, the key gameplay-relevant elements are:
- The world can be explored in two dimensions, short excursions in a third dimensions may be considered
- The world has points of interest, which are sparsely distributed and small (see gameplay/navigation below)
- There is a medium filling the world with varying density (see vessel below)
- There is no gravity, an accelerated object may move indefinitely, with only a small braking effect of the medium (small on the scale of typical distances)
- The world outside the points of interest is not survivable for the player outside the vessel

### The vessel

The vessel can move through the medium with an engine. The medium will (slightly) slow the vessel down and cause ablation on the vessels hull. These effects are higher the higher the density is.

The vessel has sophisticated technical systems with high inter-connectivity. As an example of the envisaged detail level, the systems could include:
  - A fuel system (tanks, lines, pumps, filters, valves etc.)
  - An electrical system (batteries, generators, busses, fuses, switches etc.)
  - (An) engine(s) with high-fidelity simulation (RPMs, temperatures, fuel-flow, throttle-response curves, lubrication etc.)
  - An RCS system for low-speed maneuvers (with fuel, valves, pumps etc.)
  - A hydraulics-driven control surface system for high-speed maneuvering (with pumps, pistons, lines, tanks etc.)
  - A life support system (CO2 scrubbers, O2 tanks, ventilation, control systems)
  - Radiation shielding by way of shielding tanks, in which fuel and/or water can be pumped (tanks, pumps, radiation sensors etc.)
  - A radar system (dish, power, cooling etc.)
  - Sensors for all systems
  - Auxiliary systems (lights, computers, etc.)
  - [Maybe] Weapons systems (turrets, ammunition etc.)

All systems in the vessel can be damaged or fail, including sensors (which could freeze, fail low, fail high or not read anything anymore) and displays. All failures have the expected consequences (i.e. if a bus goes offline, all connected systems stop functioning, a clogged fuel filter will lead to degraded engine performance etc.). The damage model is cascading, e.g. an overheating generator will fail eventually, disrupting the electrical system, which can take other systems offline and so on.

The ship has a low level of automation, e.g. a startup from cold&dark will involve ramping up the electrical system, enabling the fuel pumps, activating the engine starter and introducing fuel at the correct moment in the correct quantity.

The vessel provides a chart room and facilities to take positional fixes. While the math is done automatically, the process still must be done by hand. The ship does not provide an automatic navigation or moving-map type facilities.

### The players tasks

The game is envisioned for crews of 3-4 players. The players do not have fixed roles, the need for coop arises from the complexity of the systems and the amount of tasks which need to be done. One player alone could theoretically do everything, but the layout of the controls would make it arduous and no successful for any stretch of time.

### Task clusters

- Piloting (depending on actual task load, this may be split to a fourth operations/planning role)
  - The pilot controls the ship in space with the RCS system or the control surfaces.
  - He asks for thrust levels and duration from the engineer.
  - The pilot handles the communication with ATC where needed.
  - The pilot monitors the newsfeeds and selects potentially interesting targets to visit.
  - The pilot handles the crew's finances and trading when in port
- Navigation
  - The navigator plots a course and an acceleration schedule to a given target.
  - To assist in this, a linear navigation calculator is provided, which will calculate thrust levels and durations for a linear accelerate-coast-break travel. Non-linear travel is possible, but needs to be estimated without a calculator.
  - The navigator is responsible for taking positional fixes by taking bearings, adding them to the chart and finding the intersect point. If traveling at high speeds, this may have to be done by two people to reduce errors.
  - The navigator is responsible for entering the burn times and correctly timing the coast phase.
- Engineering
  - The engineer runs the technical systems of the vessel, i.e. starts the engine, sets the throttle setting etc.
  - The engineer is responsible for the center of gravity and radiation shielding by pumping fuel and consumables to the appropriate tanks and shield layers.
  - He is responsible for diagnosing failures and repairing any damage.
  - He is responsible for monitoring ablation and other wear and tear in the vessel and advising pilot and navigator accordingly.
  - The engineer advises the pilot on what parts and upgrades need to be purchased.
  - The engineer can build spare/replacement parts in case of failures.

### The overall game loop

The game starts in port, in the ship, which is reasonably equipped to start traveling. The chart shows a small region around the starting port. The game loop then runs through the following phases. Note that for simplicity, we use the roles from above, but this task distribution is not enforced by the game. It should arise naturally and may be different for each crew.

#### Port time

- The pilot checks for available missions to execute (haul freight, chart region, mine, [maybe] combat).
- The pilot buys/sells equipment/resources as needed and requested by the other crew members.
- The pilot selects a target and tells the navigator, who works out a route depending on available fuel, time constraints, shielding status, and weather reports.
- The engineer works on systems which can only be taken offline in port.
- The engineer takes in deliveries and stows them appropriately (i.e. exchanges empty oxygen tanks against new ones, re-fills hydraulics systems etc.).

#### Getting underway

- The pilot coordinates a departure slot with ATC.
- The navigator enters the appropriate information into the corresponding systems, giving the pilot his navigational cues and the engineer the appropriate burn time and thrust.
- The engineer starts up the systems and engines together with the other crew members.
- The engineer coordinates the disconnection of the umbilicals.
- The pilot asks for disconnection of the docking clamps and moves the vessel away from the port.

#### Travel

- The acceleration burn is executed in coordination by the pilot (direction), the engineer (thrust) and the navigator (timing).
- In the coast phase
  - The engineer monitors the vessel's system, i.e. radiation, consumption, efficiency, failures etc.
  - The pilot monitors communication, i.e. weather and other danger reports, and the correct spacecraft attitude.
  - The navigator checks direction, speed, and position regularly and asks for corrections if needed.
- Travel should take 5-15 minutes real time, depending on the distance to be traveled.
- During travel, there can be wind in the medium, which needs to be monitored by the navigator. Occasionally, a storm can occur, blowing the vessel off-course and/or damaging systems. Shield ablation must be monitored, as medium density may fluctuate vs. the charts, or in uncharted territory, unexpectedly high density may require braking or even reversing and trying a different course.
- Usually, traveling to a destination will require 2-3 legs to circumvent storm, high-density areas or other risks

#### Destination

- Travel targets are small, so if navigation was not precise or conditions were not as expected, an additional leg may be required.
- Depending on destination, there may be an additional correction burn needed to find the target.
- If the destination is a port, the loop can start again. Other possible destinations could be
  - Ships in distress
  - Asteroids-like objects which can be mined by setting up mining equipment (similar complexity as the vessel).
  - Alien relics to be explored.
- If the vessel has taken damage, a shutdown and repair at the destination may be necessary to diagnose and repair.
- [Maybe] combat
  - Combat could add an element of excitement and pressure.
  - In combat, the navigator would be a gunner, the ship would be strained and could take complex damage.
  - The engineer would have to keep shielding and engines running despite damage.
  - As combat can be very costly, fleeing should be considered as a viable option. This could result in becoming lost and may cost a lot of fuel.

## Open questions

At this stage of the concept, there are a number of open questions which should be explored in a demonstrator before committing to anything more, including
- Is navigation actually fun?
- Is engineering too difficult?
- Is combat needed?
- What is the optimal crew size?
- How much uncertainty is enjoyable?
- Can players meaningfully disagree with each other?

## License

Copyright © 2026 Karl Bicker

This work is licensed under the Creative Commons Attribution 4.0 International License (CC BY 4.0).

You are free to share, adapt, and build upon this work, including for commercial purposes, provided appropriate attribution is given.

https://creativecommons.org/licenses/by/4.0/
