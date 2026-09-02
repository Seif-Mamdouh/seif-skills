---
name: microworld
description: Use when the user wants to understand something they're building by interacting with it instead of reading about it — /microworld, "make a micro world of this diff/feature/plan", "help me see what this change actually does", or when a change's behavior is too abstract to grasp from the code.
---

# MicroWorld

## Overview

Turn the thing being built into a Papert-style micro-world: a small, safe, interactive simulation the user learns by manipulating. Objects to think with, not documentation to read. The world is the explanation — if it needs an essay beside it, the world has failed.

Fidelity is not the goal; manipulability is. Extract the few state variables whose interactions surprise people, make those visible, and let the user turn the valves.

## Input

- `/microworld` (no argument) → model the current branch's own work. `git diff <main-branch>...HEAD` overstates this when local main is stale — isolate the branch's real change with `git log --no-merges --author=<user>` (or the branch name's intent) before modeling, and exclude merge noise.
- `/microworld <target>` → target may be a feature name, a plan/spec file, a subsystem, a PR number, or a pasted idea.

## Process

1. **Extract the model, not the code.** From the target, identify:
   - the *entities* — the 3–7 domain objects that carry state (appointments, messages, segments — never files or functions),
   - the *actions* — events the user can fire that change that state,
   - the *rules* — the transitions and invariants connecting them,
   - the *surprise* — the one non-obvious behavior the builder most needs to internalize.

   If the target is pure refactoring with no behavioral model, say so and ask what to model instead.

2. **State the world design in chat before building** (a few lines): entities with their visible state, the actions offered, the surprise it will expose, and three "things to try." This is the checkpoint where a wrong model gets caught cheaply. If running non-interactively (no one can answer), state the design anyway, proceed, and flag the unverified model in the final report.

3. **Build one self-contained interactive HTML page.** Load the `artifact-design` skill first; load `dataviz` if the world includes any chart. Give the page a distinctive name-style `<title>` and put the three "things to try" in the world itself. Meet every World Requirement below.

4. **Publish as a private Artifact** (stable favicon). Deliver the link plus the three "things to try" repeated in chat — no explanation essay.

## World Requirements

- **User drives.** Nothing moves until the user acts. No autoplay, no tour that advances itself.
- **Visible state.** Every piece of state the real system hides (queue depth, flags, cursors, retry counts) gets a visual representation that updates live.
- **Immediate consequences.** Every action shows its effect in the same interaction — animate the transition if the causality isn't obvious.
- **Safe to break.** A Reset button. Invite weird inputs; wrong moves should produce *interesting* visible failures, not disabled buttons.
- **Low floor, high ceiling.** The first click is obvious within five seconds; deeper knobs (edge-case toggles, timing controls, load sliders) reward continued play.
- **Self-contained.** Artifact CSP allows no external resources — inline everything.

## Common Mistakes

- **Slideshow disguised as a world.** A step-through walkthrough is presentation, not a micro-world. Test: can the user do something the author didn't script and see an honest consequence?
- **Simulating the codebase instead of the domain.** Boxes named after services and files teach architecture trivia. Model what the system is *about*.
- **Prose leakage.** Paragraphs next to the simulation mean the simulation isn't carrying the load. Keep text to labels, tooltips, one-line in-world annotations (a dimmed table may say why it's dimmed), and the things-to-try list.
- **Too many tanks.** More than ~7 stateful entities and the surprise drowns. Cut until every remaining element earns its place.
