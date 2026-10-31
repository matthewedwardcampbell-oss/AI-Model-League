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

## III. The First Experiment

A cheap, runnable test. Full protocol in [`docs/experiment-protocol.md`](docs/experiment-protocol.md).

1. Pull 4–6 small fine-tunes sharing one base (e.g., Mistral-7B family).
2. Score each on a benchmark — the tournament.
3. Merge the **bottom** cohort (hypothesis) and the **top** cohort (control).
4. Re-score both offspring.
5. **Win:** merged underdogs beat their parents. **Fail:** regression to the mean.
   Either outcome is a real result.

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

### 2. Cybersecurity *(Defensive Research — Air-Gapped, Contained)*

Framed strictly as contained, defensive research on a fully air-gapped range with no path
to the open internet. Containment is the point; CFAA and dual-use proliferation risk are
explicit constraints. This studies defense and containment — it is **not** a builder of
autonomous attackers.

- **Red** — contained vulnerability discovery + payload testing against designated
  sandboxes only.
- **Orange** — creative attack mutation; bypasses static pattern detection.
- **Silver** — offensive containment at the hypervisor; enforces air-gap, kills rogue
  egress, prevents lateral movement.
- **Blue** — frontline defense; log analysis, real-time rules, automated patching.
- **Green** — chaos injection (misconfigs, resource starvation, container restarts).
- **Gold** — defensive invariant enforcement; blocks Blue "reward hacking" (no winning by
  killing the server or deleting databases).
- **Purple** — neutral arbiter; chess-clock stepping, breach/patch scoring, triggers
  DARE/TIES merges between rounds.

### 3. Macroeconomic & Planetary Climate Modeling *(AB-IAM)*

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

### 4. Circular Resource Recovery & Social Enterprise *(Joy's Kitchen Hub)*

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
