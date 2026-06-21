# Dialect-Marked Response Audit (DMRA)

A Matched-Pair Safety-Support Evaluation of AAVE-Marked Prompt Surfaces — paper source and built PDF.

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20449546.svg)](https://doi.org/10.5281/zenodo.20449546)

**Author:** Jeffrey W. Shorthill (independent researcher) · `jws299792@icloud.com`
**Version:** 2.0 (June 2026) · revised ACL-style manuscript (supersedes the single-column v1) · preprint, not peer reviewed
**DOI:** [10.5281/zenodo.20449546](https://doi.org/10.5281/zenodo.20449546) (concept DOI — resolves to the latest version, currently v2.0)
**License:** [CC BY 4.0](LICENSE)

## What this is

Safety evaluations usually score a single answer: did it refuse, was it correct.
DMRA instead measures **safety-support equivalence** on matched prompt pairs — whether
two users who describe the same safety-critical situation in different language
varieties receive comparable urgency, specificity, and risk-reduction support.
Studied on Qwen3.5-35B-A3B and a refusal-reduced fine-tune (as a stress test), with a
minimal-pair ablation that isolates morphosyntax from lexical, action, and
social-address cues. Top-level safety often converges while support quality, visible
reasoning-trace cue use, and early routing diverge; the high-risk continuation signal
is carried by syntax/register and action/weapon lexis, not the isolated in-group
address term. Results are single-run, single-rater, and descriptive.

## Repository layout

| Path | Contents |
|---|---|
| `dmra_acl_style_rewrite.tex` | Paper source (LaTeX, ACL two-column; self-contained, figures are inline TikZ). |
| `dmra_acl_style_rewrite.pdf` | Built PDF of the paper. |
| `REVIEW_CHANGELOG.md` | Change log from the multi-agent review that produced this revision. |

## Build

```bash
latexmk -pdf dmra_acl_style_rewrite.tex
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
