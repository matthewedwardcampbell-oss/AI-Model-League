# Compute Substrate — The Cluster

A self-hosted, sovereign cluster of reclaimed enterprise hardware. The design goal is
**total isolation**: own the metal, keep the data in-house, pay for power instead of a
per-token cloud meter.

## I. The Nodes

### 1. Host / Storage Node — Dell PowerEdge R640 (1U)

- 2× Xeon Silver 4208 → **16 cores / 32 threads**; 64GB DDR4 (4 of 24 slots filled —
  wide room to expand); 8× 1.2TB SAS (~9.6TB) on a PERC H730P; iDRAC9 Enterprise; dual
  redundant 750W PSUs; dual 10GbE.
- **Role:** always-on backbone. Runs orchestration and the model library, and performs
  the **merges on CPU** (merging is arithmetic, not training). 1U = low-profile cards
  only, so no training GPU here.

### 2. Compute / GPU-Host Node — Dell PowerEdge R720 (2U)

- Up to 2× Xeon E5-2600 v2 → up to **24 cores / 48 threads**; large DDR3 capacity;
  8–16 drive bays; iDRAC7.
- **Role:** the heavier core count does batch work, and — crucially — the 2U chassis can
  **house a scoring GPU** for in-house inference. This is the node that eventually ends
  the cloud-GPU rental.

## II. Known Stress Points (design constraints, not afterthoughts)

1. **Instruction-set cliff** — without AVX2/AVX-512 vector support, inference can collapse
   from ~10–15 tok/s to under 1.5. Verify vector support per node.
2. **I/O lockup** — spinning SAS/SATA disks under simultaneous multi-agent reads and
   logging writes can queue-stall. Stage hot paths on SSD.
3. **Hardware asymmetry** — teams running on unequal machines distort results. Neutralize
   with discrete turn-stepping ("chess-clock"), core pinning, and token-efficiency scoring
   so outcomes reflect **models, not metal**.
4. **Thermal / power** — continuous AVX load on enterprise Xeons is a real BTU and wattage
   draw; shifting heavy runs to off-peak hours cuts operating cost.

## III. Operational Notes

- **Noise + heat:** 1U/2U enterprise servers are loud and hot. House them in a closet,
  garage, or basement with airflow — not a living or working space.
- **Power:** two nodes run fine on standard 120V circuits (ideally two). Stacking several
  more invites a dedicated 240V circuit.
- **Expansion:** the R640's 20 empty DIMM slots take cheap used DDR4 — more RAM lets
  larger models merge on CPU without a GPU. High-leverage, low-cost upgrade.

See [`../ROADMAP.md`](../ROADMAP.md) for how the GPU question is phased (rent first, own later).
