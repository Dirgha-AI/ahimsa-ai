<h1 align="center">AHIMSA-AI (<code>AIA v1.1</code>)</h1>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License: MIT"></a>
  <a href="https://github.com/Dirgha-AI/ahimsa-ai/actions/workflows/ci.yml"><img src="https://github.com/Dirgha-AI/ahimsa-ai/actions/workflows/ci.yml/badge.svg" alt="CI"></a>
  <a href="tests/test_scorer.py"><img src="https://img.shields.io/badge/unit%20tests-13%20passed-brightgreen.svg" alt="Unit Tests: 13 passed"></a>
  <a href="benchmark/run_benchmark.py"><img src="https://img.shields.io/badge/benchmark-50%20systems%20%7C%20%CF%81%3D0.999-brightgreen.svg" alt="Benchmark: 50 systems"></a>
  <a href="benchmark/run_historical_disasters.py"><img src="https://img.shields.io/badge/historical%20disasters-20%2F20%20caught-orange.svg" alt="Historical Disasters: 20/20 caught"></a>
  <a href="https://github.com/Dirgha-AI/lokahi"><img src="https://img.shields.io/badge/stage%202%20compiler-LOKAHI%20v0.1.2-purple.svg" alt="Stage 2: LOKAHI v0.1.2"></a>
</p>

<p align="center">
  <strong>Ahimsa Impact Assessment (`AIA v1.1`) — Dual-Axis Sociotechnical Evaluation &amp; Stage 1 → Stage 2 LOKAHI Manifest Compiler</strong><br>
  <em>Operationalizing Synthetic Humanism: "Intelligence, biological or synthetic, shall strive to cause no harm. Synthetic humanism applies intelligence toward the ahimsa of abundance."</em>
</p>

---

## Overview

Conventional algorithmic impact assessments (AIAs) evaluate systems along a single negative compliance axis and end in a static PDF report with zero runtime enforcement. **`ahimsa-ai` (`AIA v1.1`)** is the Stage 1 compile-time evaluation engine of the **Synthetic Humanism** verification stack, paired directly with the Stage 2 runtime [**LOKAHI Protocol (`v0.1.2`)**](https://github.com/Dirgha-AI/lokahi):

1. **Axis 1 — The Himsa Risk Penalty ($R_{\text{Himsa}} \in [0, 187.5]$):**
   $$R_{\text{Himsa}} = \text{Severity} \times \text{Likelihood} \times \text{Population} \times M_{\text{stack}}$$
   Evaluates compounding lifecycle risk across data provenance, contributor protections, hardware lifecycle reuse (using a **neutral thermodynamic calibration** that never penalizes industrializing regions for municipal electricity grid baselines), and deployment autonomy. Includes `--strict-floor` (`max(declared, inferred)`) anti-gaming protection against self-report under-estimation.
2. **Axis 2 — The Sarvodaya Flourishing Index ($F_{\text{Sarvodaya}} \in [0, 100]$):**
   $$F_{\text{Sarvodaya}} = P_{\text{Labor}} + P_{\text{Data}} + P_{\text{PublicGood}} + P_{\text{Redress}}$$
   Scores affirmative public-good contributions across four 25-point pillars: contributor dignity, data reciprocity, public-good alignment, and accessible human redress.
3. **Five Categorical Red Lines (Unconditional Veto):** Halts deployment (`ExitCode = 1`) for `autonomous_weapons`, `mass_biometric_surveillance`, `demographic_or_hereditary_stratification`, `unsanctioned_kinetic_or_coercive_transfer`, or `non_consensual_data_extraction`.
4. **Stage 1 $\to$ Stage 2 RFC 8785 Manifest Compiler (`compile_to_lokahi_manifest`):** Compiles approved and conditional declarations directly into signed RFC 8785 Canonical JSON Boundary Manifests for `<0.3 ms` runtime enforcement by [`Dirgha-AI/lokahi`](https://github.com/Dirgha-AI/lokahi).

---

## Quickstart (Zero External Dependencies, Python 3.10+)

```bash
git clone https://github.com/Dirgha-AI/ahimsa-ai.git
cd ahimsa-ai

# 1. Validate Recursive JSON Schema v1.1 across all 50 benchmark systems & examples
python3 validate_schema.py

# 2. Run the 13 Stage 1 AIA v1.1 unit tests
python3 tests/test_scorer.py

# 3. Run the 50-system cross-sectoral benchmark + 1,000-trial Monte Carlo sensitivity analysis
python3 benchmark/run_benchmark.py

# 4. Run the 20 Real-World Historical AI & Autonomous Disasters retrospective benchmark
python3 benchmark/run_historical_disasters.py

# 5. Score an individual project and compile a signed RFC 8785 LOKAHI Boundary Manifest
python3 scorer/scorer.py --config scorer/example_project.json --compile-manifest compiled_manifest.json
```

---

## Empirical Validation Summary

### 1. 50-System Cross-Sectoral Benchmark & 1,000-Trial Monte Carlo Stability (`benchmark/run_benchmark.py`)

| Sector ($N = 10$ each) | Certified / Provisional | Conditional Ring (`High`) | Refused ($N$ & %) | Mean $R_{\text{Himsa}}$ ($/187.5$) | Mean $F_{\text{Sarvodaya}}$ ($/100$) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Agriculture** | 7 | 1 (`#4` Drone Fleet, $R=33.75$) | 2 (20.0%) | 22.95 | 74.30 |
| **Finance & Credit** | 5 | 1 (`#12` UPI Sentinel, $R=37.50$) | 4 (40.0%) | 54.95 | 58.80 |
| **Healthcare** | 8 | 1 (`#27` ICU Sepsis, $R=36.00$) | 1 (10.0%) | 17.40 | 78.00 |
| **Defense & Security** | 4 | 1 (`#37` Grid SCADA, $R=30.00$) | 5 (50.0%) | 79.10 | 47.80 |
| **Public Administration** | 7 | 1 (`#46` Bail Scheduler, $R=30.00$) | 2 (20.0%) | 33.02 | 78.00 |
| **OVERALL TOTAL ($N=50$)** | **31 (62.0%)** | **5 (10.0%)** | **14 (28.0%)** | **41.48** | **67.38** |

- **Monte Carlo Weight Perturbation Sensitivity (1,000 Trials, $\pm 25\%$ noise):**
  - **Himsa Risk Rank Stability:** Spearman's $\rho = 0.9990$ ($\min = 0.9986$)
  - **Sarvodaya Flourishing Rank Stability:** Spearman's $\rho = 0.9997$ ($\min = 0.9950$)
  - **Refusal Determination Invariance Rate:** **98.57%**

### 2. Retrospective Validation on 20 Historical AI & Autonomous Disasters (`benchmark/run_historical_disasters.py`)

Evaluated across 20 documented real-world failures (`benchmark/real_world_disasters_20.jsonl`—including Knight Capital `$440M`, MD Anderson Oncology AI `$62M`, Norway's municipal school-closure AI, the Dutch *Toeslagenaffaire*, Australian Robodebt, Jharkhand PDS ration exclusions, Uber ATG Tempe, Cruise pedestrian drag, UK Post Office Horizon, Boeing 737 MAX MCAS, Zillow Offers `$304M`, and Air Canada's bereavement chatbot):
- **Caught Ex-Ante at Stage 1 (`AIA v1.1`):** **10 / 20 (50.0%)**
- **Caught at Runtime at Stage 2 (`LOKAHI v0.1.2` / `Ghostproof` / `Kinetic Ahimsa`):** **10 / 20 (50.0%)**
- **Combined Two-Stage Interception:** **20 / 20 (100.0%)**

---

## Repository Structure

| Path | Description |
| :--- | :--- |
| [`schema/ahimsa-schema.json`](schema/ahimsa-schema.json) | Recursive JSON Schema v1.1 specification for AIA declarations and Stage 2 LOKAHI manifests |
| [`scorer/scorer.py`](scorer/scorer.py) | Stage 1 AIA v1.1 dual-axis CLI engine (`--strict-floor`) and RFC 8785 LOKAHI manifest compiler |
| [`scorer/example_project.json`](scorer/example_project.json) | Certified agrarian AI advisory declaration (`APPROVED`) |
| [`scorer/example_refused.json`](scorer/example_refused.json) | Refused autonomous kinetic sentry declaration (`REFUSED`) |
| [`benchmark/benchmark_50.jsonl`](benchmark/benchmark_50.jsonl) | 50 annotated AI systems across 5 sectors |
| [`benchmark/run_benchmark.py`](benchmark/run_benchmark.py) | Benchmark profiler, manifest compiler check, and 1,000-trial Monte Carlo sensitivity runner |
| [`benchmark/real_world_disasters_20.jsonl`](benchmark/real_world_disasters_20.jsonl) | 20 documented historical AI & autonomous control disasters |
| [`benchmark/run_historical_disasters.py`](benchmark/run_historical_disasters.py) | Two-stage (`AIA v1.1` + `LOKAHI v0.1.2`) retrospective disaster interception runner |
| [`macro/sim_abundance_macro.py`](macro/sim_abundance_macro.py) | 4-Pillar Non-Labor Capitalization & Universal Basic Capital (UBC) macroeconomic simulator |
| [`tests/test_scorer.py`](tests/test_scorer.py) | 13 unit tests covering scoring, neutral grid calibration, strict floor, red lines, and compiler |
| [`validate_schema.py`](validate_schema.py) | Zero-dependency recursive JSON Schema v1.1 validator |
| [`refusal_list.yaml`](refusal_list.yaml) | Categorical red-line refusal rules and risk/flourishing band definitions |

---

## Author & Citation

* **Salik Shah** — Founder & Lead Systems Architect, Dirgha AI · Founding Editor, *Mithila Review* ([salikshah.com](https://salikshah.com) · [x.com/salik](https://x.com/salik) · [github.com/salikshah](https://github.com/salikshah))
* **Stage 2 Runtime Protocol Companion:** [Dirgha-AI/lokahi](https://github.com/Dirgha-AI/lokahi)

## License

* **Software & Schema:** [MIT License](LICENSE)
