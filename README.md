# mimo-spatial-filtering

**Spatial signal processing in a 4 × 64 MIMO–OFDM system: SVD precoding, uniform precoding, beam-domain visualization, and the cost of imperfect CSI on downlink spectral efficiency.**

A NumPy/SciPy MIMO link-level simulator that characterizes the spatial structure of measured MIMO channels and quantifies how channel-estimation noise degrades the achievable rate of an SVD-precoded downlink.

## What this project investigates

Given a measured MIMO channel realization `H ∈ ℂ^(M × N × K × T)` with
- `M = 4` UE antennas,
- `N = 64` BS antennas,
- `K = 600` OFDM subcarriers,
- `T = 100` time instants,

the project answers three concrete questions:

1. **What does the spatial structure of this channel actually look like?** — angular/beam-domain spectrum, distribution of singular values across time–frequency resources.
2. **How much does SVD-based precoding beat a uniform precoder?** — head-to-head spectral-efficiency CDFs at varying transmission ranks.
3. **How much does CSI error cost you?** — re-run the precoding pipeline on noisy channel estimates and quantify the spectral-efficiency loss vs. ideal CSI as a function of uplink SNR.

## Method (short version)

- Spectral efficiency per (subcarrier, TTI) is computed as
  `C(k,t) = log₂ det(I + (ρ/R) · H · W · Wᴴ · Hᴴ)`,
  where `W` is the precoder of rank `R` and `ρ` is the downlink SNR.
- Two precoders compared:
  - **SVD precoder** (optimal for known CSI in the spectral-efficiency sense),
  - **Uniform precoder** (baseline).
- CSI errors modeled as additive complex Gaussian noise on `H` at controlled SNRs; the noisy `H` is fed to the same SVD pipeline and the resulting spectral-efficiency CDF is compared to the ideal-CSI CDF.

## What's in here

| File | Purpose |
|---|---|
| `notebooks/spatial_filtering.ipynb` | Complete notebook with all code, derivations, and figures |
| `report.pdf` | Written report (PDF — distribution-controlled; ask the author for access) |
| `LICENSE` | MIT |

## Data

The notebook loads pre-recorded MIMO channel realizations distributed as MATLAB `.mat` files (`link_chan_*.mat`, `srs_sig.mat`) by the course. These files are course-restricted and **are not included in this repository**. Place them in the directory referenced by `FOLDER_PATH` at the top of the notebook (or change that path to match your local setup).

## Running it

```bash
pip install numpy scipy matplotlib tqdm ModulationPy
```

Then open the notebook and run cells top-to-bottom. Pure NumPy/SciPy — no GPU required.

## Context

Coursework for the **MIMO Wireless Communications** course at the **Skolkovo Institute of Science and Technology (Skoltech)**, M.Sc. in IoT and Wireless Technologies.

## License

MIT — see [`LICENSE`](LICENSE).

---

*Author: Muhammad Hanzala Iqbal.*
