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
4. **Merge the complementary losers** with mergekit — start with TIES or DARE. *(hypothesis arm)*
5. **Merge a random pair of losers** with the same method. *(control arm — isolates
   orthogonality from the mere act of merging two models)*
6. **Merge the top 2–3** as a second control. *(control arm — isolates underdog from elite)*
7. **Re-score all three offspring** on the same benchmark, same settings.

## IV. Picking Complementary Losers

- **The primary signal — per-skill mirror scorecards.** Score each loser **per skill**
  (reasoning, writing, math, instruction-following), not one overall grade. Pair the ones
  with **mirror-image scorecards** — Loser A bombs what Loser B aces, and vice versa. This
  is the measure that actually tracks complementary *capability*, so it leads.
- **The sanity check — task-vector angle.** Cosine similarity between two losers' task
  vectors; near-90° reads as orthogonal. Treat it as a check, not an oracle: in very high
  dimensions almost *every* pair of vectors is already near-orthogonal, so a near-90°
  reading is the default, not the signal. Use it to flag pairs that are suspiciously
  *parallel* (redundant), not to certify that orthogonal ones are complementary.
- **Shortcut:** losers fine-tuned on *different data* tend to fail differently — seek
  variety on purpose.

## V. Reading the Result

- **Win:** the complementary-loser merge beats its own parents **and** clears the
  random-loser merge (bonus if it rivals the merged winners).
- **Fail:** it regresses to the mean, **or** it beats its parents by no more than the
  random-loser merge does — meaning the effect was "merging two models helps," not
  "orthogonality helps."

Either outcome is a real, publishable result. The two controls are what make it a result
at all: the **top-cohort** merge isolates *underdog* from *elite*, and the **random-loser**
merge isolates *orthogonality* from the mere act of merging. Without the random arm, a win
can't be attributed to the complementary-failure rule — which is the whole hypothesis.

## VI. Scope Discipline for Run #1

Keep the first run tiny — 3 models, one merge method, one small benchmark — just to prove
the pipeline end-to-end before scaling to full tournaments, evolutionary recipe search,
and the quality-diversity archive.
