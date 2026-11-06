# AI Training Channel — Autonomous Model League

> **Status:** Conceptual architecture / design document — not an implementation.
> This describes a proposed framework and the scenarios built to stress-test it.
> The core (Sections I–IV) is the testable heart; the Grand Vision (V–VII) is
> forward-looking. Feedback on the concept is the goal.

## Repository Map

- [`README.md`](README.md) — overview (this file)
- [`docs/experiment-protocol.md`](docs/experiment-protocol.md) — the first runnable experiment
- [`docs/hardware.md`](docs/hardware.md) — the self-hosted compute cluster
- [`docs/glossary.md`](docs/glossary.md) — key terms, plainly defined
- [`docs/teams-by-stage.md`](docs/teams-by-stage.md) — the color-teams applied across the training loop, the model lifecycle, and AI history
- [`ROADMAP.md`](ROADMAP.md) — phased build-out and the later layers

## I. The Core Idea

Conventional training optimizes a single model, and standard evolutionary methods
discard underperformers ("culling the weak"). This framework proposes the inverse:
rather than discarding weak checkpoints, it identifies models whose failures are
*orthogonal* — bad in different directions — and synthesizes them via task-vector
arithmetic.

**Hypothesis:** underdogs with complementary failure modes can be merged into
resilient hybrids *without backpropagation*, because merging is arithmetic on
existing weights — far cheaper than retraining. Whether this preserves useful
diversity or collapses toward the mean is the open question the framework tests.

The rule that decides it: merge losers whose weaknesses are **complementary**, not
identical. Same-direction failures average into mush; opposite-direction failures
cover each other's gaps.

## II. Weight-Space Synthesis

Post-training merging via [mergekit](https://github.com/arcee-ai/mergekit). Requires
models sharing one base lineage.

1. **DARE** — zeros a probability *p* of delta weights, scales survivors by 1/(1−p);
   clears most parameter-collision space while preserving expected magnitude.
2. **TIES** — trims low-magnitude noise, takes a directional sign-consensus, averages
   only aligned task vectors to avoid destructive interference.
3. **SLERP** — spherical interpolation preserving norm geometry across two checkpoints.
4. **Block-level / Frankenmerging** — interleaves specialist layers into depth-extended
   hybrids.
5. **MAP-Elites / Quality-Diversity** — archives lineages across multiple capability
   axes (reasoning, latency, token economy) instead of one benchmark scalar; the
   mechanism that protects diversity.

**Known ceiling.** Merging only works within one base family, so the diversity this
method can harvest is capped at *intra-family*. The most orthogonal failure modes often
live across *different* base models — which weight arithmetic cannot combine. The
complementarity available here therefore has a structural upper bound, named up front so
a reviewer doesn't find it first.

## III. The First Experiment

A cheap, runnable test. Full protocol in [`docs/experiment-protocol.md`](docs/experiment-protocol.md).

1. Pull 4–6 small fine-tunes sharing one base (e.g., Mistral-7B family).
2. Score each on a benchmark — the tournament.
3. Build **three** merge arms: the **bottom** cohort paired for *complementary* failures
   (the hypothesis); a **random** pair of losers (the control that isolates orthogonality
   from merging-at-all); and the **top** cohort (the control that isolates *underdog* from
   *elite*).
4. Re-score all three offspring.
5. **Win:** the complementary-loser merge beats its parents *and* clears the random-loser
   merge. **Fail:** it regresses to the mean, or beats its parents by no more than the
   random pair does — in which case the effect is "merging helps," not "orthogonality
   helps." Either outcome is a real result.

## IV. Compute Substrate

A self-hosted, sovereign cluster of reclaimed enterprise hardware. Detail in
[`docs/hardware.md`](docs/hardware.md).

1. **Host / storage node** (Dell R640) — always-on; runs orchestration, holds the model
   library, runs merges on CPU (merging is arithmetic, not training).
2. **Compute / GPU-host node** (Dell R720, 2U) — higher core count; the chassis that can
   house a scoring GPU for in-house inference.
3. Known stress points (design constraints, not afterthoughts): the AVX2/AVX-512
   instruction-set cliff, I/O lockup on spinning disks, hardware asymmetry between nodes,
   and thermal/power load. See the hardware doc.

---

# The Grand Vision (Exploratory)

*Forward-looking: how far the generate-vs-contain-vs-merge pattern might reach, and the
open questions each raises. Not implemented.*

## V. The Color-Team Architecture

**Origin:** this system emerged from a multi-agent **game-design engine** — competing
creative agents generating a game's art, lore, and economy, held in check by containment
agents acting as art directors and QA. That generate-vs-contain dynamic is the reusable
pattern; each domain below fields its own tailored team.

## VI. Applications & Stress-Test Scenarios

### 1. Game Design & Narrative *(origin domain)*

- **Red** — asset generation + exploit hunting (biomes, units, broken economy loops).
- **Orange** — aesthetic mutation + emergent/off-meta playstyles.
- **Silver** — art & style-bible gatekeeper; flags visual drift.
- **Blue** — asset normalization + core economy/balance pacing.
- **Green** — readability + edge-case stress (UI downscaling, chaotic matchups).
- **Gold** — engine invariant guard (rejects non-power-of-two, alpha bleed, broken
  mipmaps; blocks over-nerfing that sterilizes play).
- **Purple** — lore-canon arbiter + balance synthesizer (merges nerf vs emergent-play
  models).

### 2. Macroeconomic & Planetary Climate Modeling *(AB-IAM)*

A bottom-up agent economy rather than top-down static equations (DSGE).

- **Red** — speculative capital; leverage, shorting, cornering, bubbles.
- **Orange** — irrational retail; herd behavior, panic selling, hoarding.
- **Silver** — financial circuit breakers; margin calls, halts, liquidations.
- **Blue** — industrial backbone + commercial banking; production, payroll, credit.
- **Green** — clean-tech R&D (geothermal, storage, low-carbon cement, desalination).
- **Cyan** — physical grid reality check (transmission resistance, interconnect queues,
  mineral shortages, intermittency).
- **Gold** — thermodynamic + accounting conservation; no phantom credit or hallucinated
  materials.
- **Purple** — historical precedent / institutional memory; the conservative anchor.
- **Yellow** — live telemetry + dynamic reform; forces adaptation.
- **White** — atmosphere/biosphere telemetry (heating days, rainfall deficits, soil
  depletion, emissions).
- **Black** — exogenous shock engine (Cat-5 landfalls, droughts, choke-point blockades,
  sovereign defaults).

### 3. Circular Resource Recovery & Social Enterprise *(Joy's Kitchen Hub)*

- **Red** — feedstock arbitrage; takes clean waste streams for free/nominal cost, beating
  landfill gate fees at the point of origin.
- **Orange** — community-needs telemetry; routes food/material surplus to highest need.
- **Silver** — regulatory compliance (HACCP, food-safety codes, fair labor).
- **Blue** — processing backbone; upcycles perishables to shelf-stable goods, runs
  recycling machinery.
- **Green** — workforce development; low-barrier visual SOPs, ServSafe, shift meals for
  unhoused/refugee workers.
- **Gold** — unit economics; dual-market model subsidizes low-cost staples, avoids the
  charity-dependency trap.
- **Purple** — closed-loop lead; routes server exhaust heat to winter aeroponics, kitchen
  trimmings to biogas; also explores shared community compute on the reclaimed cluster.

## VII. Status

Sections I–IV are the implemented/testable core. Sections V–VII are a research vision: a
map of where the pattern might reach and the failure modes each path must survive. Listed
to be pressure-tested, not claimed as working systems.
