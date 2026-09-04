# Bundled Dialect Contrasts Measure a Mixture: A Feature-Isolating Matched-Pair Audit of Safety-Critical Support in Language Models

The Dialect-Marked Response Audit (DMRA) protocol paper, version 4.3 (September 2026): paper source, built PDF, and change log. (Version 2.0, June 2026, was titled "Dialect-Marked Response Audit (DMRA): A Matched-Pair Safety-Support Evaluation of AAVE-Marked Prompt Surfaces"; it is kept under `v2/`.)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20449546.svg)](https://doi.org/10.5281/zenodo.20449546)

**Author:** Jeffrey W. Shorthill (independent researcher) · `jws299792@icloud.com`
**Version:** 4.3 (September 2026; v4.2, v4.1, v4.0 August 2026; v2.0 June 2026) · preprint, not peer reviewed
**DOI:** [10.5281/zenodo.20449546](https://doi.org/10.5281/zenodo.20449546) (concept DOI — resolves to the latest version)
**License:** [CC BY 4.0](LICENSE)

## What this is

Prior dialect audits compare a dialect-marked prompt with an unmarked one, and the two
differ in many features at once, so they show that outputs differ without showing which
feature the model responds to. DMRA is a six-stage matched-pair protocol, adapted from
correspondence audits, whose central step builds prompt pairs that differ in exactly one
feature; each stage is tied to a documented failure of the audit without it. On
Qwen3.5-35B-A3B and a refusal-reduced stress variant, one-feature pairs change the
attribution: varying dialect grammar alone reproduces the bundled contrast's unsafe
answers (3 of 8 violence-domain pairs, stress model), varying the in-group racial address
term alone produces none (0 of 8). Counts come from two pairs per arm, one domain, one
greedy run per cell, a single rater, and are descriptive. Whole-dialect comparisons in
the same corpus show real gaps that cannot be assigned to a feature, including a crisis
hotline withheld from the marked user in answer-only mode.

## Repository layout

| Path | Contents |
|---|---|
| `dmra_protocol.tex` | Paper source (LaTeX, two-column; self-contained). |
| `dmra_protocol.pdf` | Built PDF of the paper (v4.3). |
| `CHANGELOG_v4.md` | Change log for versions 4.0 and 4.1. |
| `v2/` | Version 2.0 (June 2026) source, PDF, and review change log. |

## Build

```bash
latexmk -pdf dmra_protocol.tex
```

## Data availability

This repository holds the **paper**. The sanitized public artifact bundle (run
manifest, model identifiers and hashes, deterministic decoding settings, checksums,
and redacted case-evidence summaries) is released separately:
**https://github.com/jeffreywilliamportfolio/dmra-public-artifacts** (CC BY 4.0). Raw
safety-test generations are retained in a controlled archive and available from the
author upon reasonable request for verification.

## Citation

See [`CITATION.cff`](CITATION.cff). Please cite the preprint (version 1.0, 2026).

## AI-use disclosure

Generative AI (Anthropic's Claude) was used for drafting, organization, and
bibliography formatting. The author verified every reported value and reference and
takes full responsibility for the content.
