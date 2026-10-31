# Experiment Protocol — The First Run

A cheap, weekend-scale test of the core hypothesis: **can merging underdog models whose
failures are complementary produce a hybrid that beats its parents?** The only real cost
is compute, not ideas.

## I. The Principle Being Tested

Merge losers whose weaknesses are **complementary**, not identical.

- Opposite-direction failures cover each other's gaps → the merge can fill both.
- Same-direction failures just average the same weakness → collapse ("mush").

The predictor of success is **orthogonality**: two models' task vectors pointing in
different directions (near-90°) are complementary; parallel vectors are redundant.

## II. Tools

- [mergekit](https://github.com/arcee-ai/mergekit) — free, open-source; performs every
  merge method (DARE, TIES, SLERP, …) from a short config file.
- [Hugging Face](https://huggingface.co) — the open-model library the contestants come from.
- One GPU for scoring (rented by the hour in the early phase — see [`../ROADMAP.md`](../ROADMAP.md)).

**Hard rule:** all models must share **one base lineage** (e.g., several Mistral-7B
fine-tunes). You can only merge checkpoints from the same family.

## III. The Run

1. Download **4–6 small open fine-tunes sharing one base** (e.g., Mistral-7B). 7B fits a
   single 24GB card.
2. **Score each on a benchmark** → rank them. This is the tournament.
3. Take the **bottom 2–3 (losers)**; confirm their per-skill scorecards fail *differently*
   (see §IV).
4. **Merge the losers** with mergekit — start with TIES or DARE.
5. **Merge the top 2–3** as the **control group**.
6. **Re-score both offspring** on the same benchmark.

## IV. Picking Complementary Losers

- **The rigorous way:** measure the angle (cosine similarity) between two losers' task
  vectors. Near-orthogonal = complementary.
- **The practical proxy:** score each loser **per skill** (reasoning, writing, math,
  instruction-following), not one overall grade. Pair the ones with **mirror-image
  scorecards** — Loser A bombs what Loser B aces, and vice versa.
- **Shortcut:** losers fine-tuned on *different data* tend to be naturally orthogonal —
  seek variety on purpose.

## V. Reading the Result

- **Win:** the merged losers beat their own parents (bonus if they rival the merged winners).
- **Fail:** the loser-merge regresses to the mean — worse than either parent.

Either outcome is a real, publishable result. The failure case is as informative as the
success case, which is why the top-cohort control matters: it isolates whether *underdog*
merging specifically does anything.

## VI. Scope Discipline for Run #1

Keep the first run tiny — 3 models, one merge method, one small benchmark — just to prove
the pipeline end-to-end before scaling to full tournaments, evolutionary recipe search,
and the quality-diversity archive.
