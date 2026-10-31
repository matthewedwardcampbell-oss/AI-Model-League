# Glossary

Plain-language definitions for the terms used across this repo.

- **weights** — the enormous list of learned numbers inside a model; its knowledge.
- **base model** — the shared ancestor model. Merging only works between checkpoints that
  share one base lineage.
- **fine-tune** — a base model further trained on a narrower task; a specialist branch of
  the base.
- **task vector** — a fine-tune minus its base. What's left is *just the skill the
  fine-tune learned* — a portable "skill chip" you can add to another model.
- **orthogonal** — two task vectors pointing in different directions (near-90°). Orthogonal
  skills are **complementary** and good to merge; parallel skills are redundant.
- **benchmark** — a fixed test set used to score and compare models.
- **mergekit** — the open-source toolkit that performs the merges from a config file.
- **DARE (Drop And Rescale)** — drops a random fraction *p* of a task vector's weights and
  rescales the survivors by 1/(1−p) to preserve expected magnitude; reduces collision when
  stacking many merges.
- **TIES** — trims trivial weight changes, resolves sign conflicts by consensus vote, and
  averages only aligned task vectors to avoid destructive interference.
- **SLERP (Spherical Linear Interpolation)** — blends two checkpoints along a curved path
  that preserves norm geometry, rather than a flat average.
- **Frankenmerging / block-level merging** — interleaves whole layers from different
  specialists into a depth-extended hybrid.
- **evolutionary merge** — a search that evolves the *merge recipe itself* across
  generations, scoring each candidate and keeping the good ones (cf. Sakana AI, 2024).
- **MAP-Elites / Quality-Diversity** — keeps the best model in each *behavioral niche*
  rather than only the top overall scorer; the mechanism that preserves diversity instead
  of collapsing toward the mean.
- **catastrophic interference** — when merging models that fail the *same* way just
  amplifies the shared weakness, degrading the hybrid into incoherence.
