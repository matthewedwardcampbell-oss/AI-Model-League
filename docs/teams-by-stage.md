# Teams by Stage — The Framework's Generality

The color-team architecture is **scale-invariant**: the same *generate → contain → arbitrate*
loop runs inside a single merge cycle, across a model's full development lifecycle, and even
across the history of the field. This document applies the teams to each.

## I. The Recurring Cast

- **Red** — generates / probes / attacks.
- **Orange** — mutates / diversifies.
- **Blue** — builds / normalizes / defends.
- **Green** — injects chaos, edge cases, stress.
- **Silver** — contains the generators (sandbox, governance, circuit-breaker).
- **Gold** — enforces the hard invariants (anti-cheat, conservation laws, technical floor).
- **Purple** — scores, arbitrates, and remembers across cycles.
- *Domain colors* — **Cyan** (physical-constraint check), **Yellow** (live telemetry),
  **White** (planetary telemetry), **Black** (exogenous shock).

## II. Journey 1 — The Evolutionary Training Loop

The League's own engine. One turn of the wheel:

1. **Initialize the population** — gather a base model and its fine-tunes.
   - **Red** sources the candidate pool; **Orange** forces variety (diverse fine-tunes →
     orthogonal merges later).
2. **Tournament** — score every contestant.
   - **Purple** runs the chess-clock and logs scores; **Green** injects edge cases so the
     ranking isn't gamed by easy ones.
3. **Selection** — pick parents (underdogs with complementary failures).
   - **Gold** enforces the make-or-break invariant: only pair losers whose task vectors are
     orthogonal. **Purple** arbitrates final picks.
4. **Variation / merge** — DARE / TIES / SLERP.
   - **Orange** mutates the recipe; **Blue** normalizes the merged weights into a runnable model.
5. **Containment check** — before trusting the offspring.
   - **Silver** sandboxes it; **Gold** catches catastrophic interference and reward-hacking.
6. **Re-evaluate & archive** — iterate.
   - **Purple** re-scores and maintains the MAP-Elites archive (which lineages hold which
     niches), so diversity survives across generations.

## III. Journey 2 — The Model Development Lifecycle

The industrial pipeline the loop lives inside:

1. **Data** — collect and curate.
   - **Red** sources data; **Orange** diversifies; **Silver** enforces governance (PII,
     licensing); **Gold** guards integrity (no contamination or leakage).
2. **Pretraining** — build the base.
   - **Blue** constructs; **Gold** enforces compute/loss invariants.
3. **Fine-tuning / post-training** — specialize.
   - **Red / Orange** generate task capability; **Blue** normalizes. *(The League's raw
     material comes from here.)*
4. **Alignment** — make it safe and useful.
   - **Green** red-teams; **Silver** contains harmful outputs; **Gold** enforces safety
     invariants; **Purple** arbitrates value conflicts.
5. **Evaluation** — prove it.
   - **Purple** scores; **Green** injects edge cases; **Black** hits it with
     out-of-distribution shocks.
6. **Deployment** — ship it.
   - **Blue** serves; **Silver** sandboxes the runtime; **Gold** guards the misuse boundary.
7. **Monitoring** — keep it alive.
   - **Yellow** watches drift and usage; **Green** runs production chaos tests; **Purple**
     holds the long memory of prior failures.

## IV. Journey 3 — The Historical Arc of AI (as a lens)

Here the teams read history rather than staff a pipeline:

1. **Symbolic AI** (1950s–80s) — hand-coded rules. A pure **Red** era of bold claims with
   little **Gold** checking whether the approach could scale.
2. **The AI Winters** (1974–80, late 80s–90s) — **Gold and Cyan** arriving late and hard:
   the reality-check enforcing compute and combinatorial limits the **Red** hype ignored.
   History's catastrophic-interference event.
3. **Machine Learning** (1990s–2000s) — **Blue** takes over from **Red**: disciplined
   construction on statistical foundations.
4. **Deep Learning** (2012 on) — **Red** and **Blue** fuse: a capability explosion that was
   also buildable. Hype and substance aligned.
5. **Transformers & LLMs** (2017 on) — **Orange's** era: one architectural mutation
   (attention) recombined into everything, with **Purple** and **Silver** rushing in to
   arbitrate and contain.
6. **Agents & the frontier** (now) — all teams active; this project sits here. The era's
   open question is whether **Gold and Silver** (containment) can scale to match **Red**
   (capability).

**The enrichment:** every AI winter was a season the field forgot it needed **Gold**. Every
spring came when **Red** generation and **Blue/Gold** discipline arrived together. Read onto
history, the framework predicts the next bust comes when capability generation outruns
containment — the exact risk the Cybersecurity domain is built to study.

## V. The Through-Line

The teams map onto all three because they are an instance of the oldest control pattern there
is:

- Something **generates** novelty (Red / Orange),
- Something **builds** it into usable form (Blue),
- Something **stresses** it to find the breaks (Green),
- Something **contains** it so the breaks don't escape (Silver / Gold),
- Something **remembers and judges** across cycles (Purple).

That is evolution (mutation / selection / inheritance), the scientific method (hypothesize /
test / peer-review), and this League alike. The framework is, underneath, a general theory of
*how intelligence improves under pressure* — pointed here at models.
