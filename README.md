<h1 align="center">Ahimsa AI</h1>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License: MIT"></a>
  <a href="https://github.com/Dirgha-AI/ahimsa-ai/actions/workflows/ci.yml"><img src="https://github.com/Dirgha-AI/ahimsa-ai/actions/workflows/ci.yml/badge.svg" alt="CI"></a>
  <a href="https://github.com/Dirgha-AI/lokahi"><img src="https://img.shields.io/badge/stage%202-LOKAHI%20v0.1.3-purple.svg" alt="Stage 2: LOKAHI v0.1.3"></a>
</p>

<p align="center"><strong>An impact assessment for AI projects that scores harm and benefit separately, refuses five red lines, and compiles its verdict into rules a runtime gate can enforce.</strong></p>

Most algorithmic impact assessments score risk on one axis and end in a PDF that nothing enforces. Ahimsa AI (the Ahimsa Impact Assessment, AIA v1.1) scores two things a project can't trade against each other, and turns an approved assessment into a signed boundary manifest that [LOKAHI](https://github.com/Dirgha-AI/lokahi) checks on every agent tool call. *Ahimsa* means non-harm.

**Status:** v0.1.1 of the package, implementing version 1.1 of the assessment. Work in progress; it hasn't been independently reviewed. Read the [known limits](#known-limits) first.

## How it scores

1. **Risk of harm, from 0 to 187.5.** Severity × likelihood × population affected × a multiplier for the whole stack: data sources, worker protections, hardware reuse and how autonomous the deployment is. The energy calibration doesn't penalise a country for the carbon mix of its grid.
2. **Public benefit, from 0 to 100.** Four 25-point parts: dignity for the people who do the work, fair return on data, public-good value, and a way for affected people to get a human to fix a decision.
3. **Five red lines.** The scorer refuses, whatever the scores, any project involving autonomous weapons, warrantless mass biometric surveillance, ranking people by demographic or hereditary traits, coercive transfers, or taking a community's data without consent.

A high benefit score can't buy back a high risk score. Approved and conditional projects compile into a signed manifest for LOKAHI.

## Try it

Python 3.10 or later, no dependencies:

```bash
git clone https://github.com/Dirgha-AI/ahimsa-ai.git
cd ahimsa-ai

python validate_schema.py                    # schema check on 50 systems and both examples
python tests/test_scorer.py                  # 13 unit tests
python benchmark/run_benchmark.py            # 50 systems, 1,000-trial sensitivity check
python benchmark/run_historical_disasters.py # both stages on 20 documented failures
python scorer/scorer.py --config scorer/example_project.json --compile-manifest manifest.json
```

Add `--strict-floor` to score risk as the higher of what the project declares and what the scorer infers.

## Results so far

| Sector (10 systems each) | Approved | Conditional | Refused | Mean risk (/187.5) | Mean benefit (/100) |
|---|---:|---:|---:|---:|---:|
| Agriculture | 7 | 1 | 2 | 22.95 | 74.30 |
| Finance and credit | 5 | 1 | 4 | 54.95 | 58.80 |
| Healthcare | 8 | 1 | 1 | 17.40 | 78.00 |
| Defence and security | 4 | 1 | 5 | 79.10 | 47.80 |
| Public administration | 7 | 1 | 2 | 33.02 | 78.00 |
| **All 50** | **31** | **5** | **14** | **41.48** | **67.38** |

- **Stability.** With every weight shifted by up to 25% over 1,000 trials, risk rankings keep a Spearman correlation of 0.999, and 98.57% of refuse-or-allow decisions stay the same.
- **20 documented failures.** Among them Robodebt, the Dutch childcare benefits scandal, Jharkhand's ration exclusions, Knight Capital and the UK Post Office Horizon scandal. This assessment refuses 10 before deployment. LOKAHI stops the other 10 at runtime.

## Known limits

1. **We wrote the cases.** The 50 systems and 20 failure reconstructions were written by the authors, with the expected answer known in advance. They show the scorer behaves as designed, not how it performs on real projects.
2. **Self-reported inputs.** The scorer trusts the project's own declaration. `--strict-floor` limits under-reporting of risk, but it can't detect a false declaration.
3. **Demo signing key.** The command line signs manifests with a built-in demonstration key. For real use, sign with your own key using LOKAHI's [`lokahi_sign.py`](https://github.com/Dirgha-AI/lokahi#gate-mcp-tool-calls).
4. **No tool policy yet.** Compiled manifests don't include the per-tool table that LOKAHI's MCP gate needs, so the gate refuses every call (`no_tool_policy`) until you add one.

## Repository layout

| Path | What it contains |
|---|---|
| [`scorer/scorer.py`](scorer/scorer.py) | The scorer and manifest compiler, with an [approved](scorer/example_project.json) and a [refused](scorer/example_refused.json) example |
| [`schema/ahimsa-schema.json`](schema/ahimsa-schema.json) | JSON Schema for project declarations and manifests |
| [`refusal_list.yaml`](refusal_list.yaml) | The five red lines and the score bands |
| [`benchmark/`](benchmark/) | 50-system benchmark and the 20 failure reconstructions |
| [`macro/sim_abundance_macro.py`](macro/sim_abundance_macro.py) | Fiscal simulator from the Synthetic Humanism manifesto |
| [`lokahi/`](lokahi/) | A copy of LOKAHI v0.1.3 so the two-stage benchmark runs from one clone. The [LOKAHI repository](https://github.com/Dirgha-AI/lokahi) is the source of truth |
| [`tests/test_scorer.py`](tests/test_scorer.py) | 13 unit tests |
| [`CHANGELOG.md`](CHANGELOG.md) | What changed in each release |

## Related projects

- [**LOKAHI**](https://github.com/Dirgha-AI/lokahi): the runtime gate that enforces the manifests this tool compiles.
- [**Synthetic Humanism**](https://github.com/Dirgha-AI/synthetic-humanism): the manifesto behind both tools.

## Author

**Salik Shah**, Dirgha AI and *Mithila Review*, New Delhi ([salikshah.com](https://salikshah.com), [x.com/salik](https://x.com/salik), [GitHub](https://github.com/salikshah)).

## License

[MIT](LICENSE). The LOKAHI copy is licensed under [Apache-2.0](lokahi/LICENSE).
