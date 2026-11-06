# Roadmap

A phased build-out. Each monetization or power layer attaches to a **working, owned rig** —
none of them come before the result.

## I. The Phases

### 1. Phase 1 — Nascent (rent)

The R640 runs the merges and holds the models; rent a cloud GPU by the hour only for the
scoring bursts. Near-zero commitment while the idea is still being proven. Isolation isn't
needed yet — the models merged are public open-weight models and the benchmarks are public,
so nothing original leaves your walls.

### 2. Phase 2 — Proven (own, local)

Once the pipeline works and the models mature into something worth protecting, bring the
GPU in-house (the R720 hosts it) and go air-gapped. The trigger to buy is *"the models are
now mine and they matter,"* not a date.

### 3. Phase 3+ — Scale & Sustain

Owned, isolated cluster. The later layers below bolt on here.

## II. The Compute Budget

The cost here is **scoring**, not merging. Merges run free on the R640's CPU; every dollar
is GPU-hours spent *evaluating* models. Rough rate: a 24GB cloud card (RTX 4090 / A10 / L4
class) is ~$0.30–0.70/hr on community marketplaces (Vast, Runpod). Budget by the number of
**re-scores**, because that is the thing that scales.

### 1. Phase 1 ceiling — prove the hypothesis

- **Run #1** (3 models, 1 method, 1 small benchmark): a few GPU-hours, fumbling included.
  **~$10–20.** Effectively free.
- **Full first tournament** (6 models, per-skill scoring, a few recipes, re-score the three
  offspring): ~20–60 GPU-hours. **~$20–50.**
- **Evolutionary recipe search** (the balloon): each generation re-scores many candidate
  merges — hundreds of re-scores per run. A serious search is **200–1,000 GPU-hours →
  $100–700 per run.** This is the line item that runs away if unwatched.
- **Hard phase ceiling: ~$500.** If $500 of scoring has gone by and the complementary-loser
  merge still hasn't cleared the random-loser control, the hypothesis isn't paying off at
  this scale — that's a stop-or-pivot signal, not a reason to spend more.

### 2. Phase 2 trigger — own vs. rent

- Buy a GPU only when both are true: the result is validated, **and** projected scoring
  volume beats the break-even on owning.
- Break-even: a used 24GB card (RTX 3090, ~$700–900) against $0.40/hr cloud is **~2,000
  GPU-hours to pay for itself**, before power. Below that, renting is cheaper and keeps the
  capital free. Don't cross the line on faith.
- Ceiling: **~$1,000–2,000** for one capable card plus the PSU and cooling to host it in the
  R720. One GPU. No multi-GPU until *revenue*, not capital, is paying for it.

### 3. Phase 3 — revenue-funded only

Past Phase 2, no personal capital. The income, capital, and power layers below fund
themselves, or they wait.

## III. Later Layers

- **Idle income — rent the GPU out.** When the card is idle, rent it on an AI-compute
  marketplace for other people's inference work. Real demand; beats mining.
  - *Bitcoin note:* GPUs cannot mine Bitcoin (ASIC-only), and GPU mining broadly died when
    Ethereum went proof-of-stake in 2022. At home power rates it loses money — don't count
    on mining to offset the rig.
- **Venture capital — raise on a result, not a pitch.** Nobody funds "an idea about merging
  losers." They fund "I merged losers with orthogonal failures and the offspring beat both
  parents — here's the benchmark." The cheap first experiment is the first slide of the deck.
- **Renewable power — grid-tied solar.** Compute is a constant 24/7 load — the hardest
  profile for solar. "As renewable as possible" realistically means grid-tied solar (panels
  offset consumption; the grid is the infinite battery via net metering). True off-grid 24/7
  needs oversized panels plus a large battery bank — a real capital project.

## IV. The Through-Line

Rent-and-prove now → own-and-isolate when the models matter → monetize and sustainably power
once there's something real to run. The income, capital, and power layers all follow the
result; none precede it.
