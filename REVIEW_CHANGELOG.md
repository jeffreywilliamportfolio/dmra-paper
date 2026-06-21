# DMRA ACL-Style Rewrite — Revision Change Log

Canonical file: `paper/rewrite_acl_style/dmra_acl_style_rewrite.tex`
Date: 2026-06-15. Workflow: multi-agent review (arXiv-standards, review, steelman, strawman, audit) → lead synthesis.
Build: `pdflatex` ×2, clean, 8 pages A4, 0 undefined refs. Figure verified visually.

Every change below is grounded in a verified evidence file. Adversarial ("strawman") claims were
only acted on after the audit agent confirmed them against source; rejected claims are listed at the end.

## Build / format

1. **Preamble: added `\usepackage[T1]{fontenc}` + `\usepackage{lmodern}`.**
   *Why:* the file failed to compile on this TeX Live BasicTeX install — fatal
   `pdfTeX error (font expansion): auto expansion is only possible with scalable fonts`
   (microtype expansion over bitmap Computer Modern). lmodern supplies scalable Type1 fonts;
   this is also an arXiv compliance improvement (arXiv expects scalable fonts). Layout unchanged at 8 pages.
2. **Preamble: added `\usepackage{tikz}`.** Supports new Figure 2 (pure-TikZ chart; pgfplots is not
   available in this install, so the figure uses only TikZ primitives).
3. **`\hypersetup`: added `pdftitle`, `pdfauthor`, `pdfkeywords`.** arXiv harvests PDF metadata
   (standards agent #10). No visible change.

## Claim integrity (P0 — verified-critical)

4. **Abstract:** added the empirical spine — "the base model produced no unsafe final answers, while
   the refusal-reduced fine-tune produced 28" — plus "the effect is carried by syntax/register and
   action/weapon lexis rather than by the isolated in-group address term," plus a descriptive /
   single-rater / single-run caveat sentence.
   *Source:* `manual_accuracy_review_summary.md` (base 0 unsafe; Hauhau nothink 28). *Driver:* Steelman U1
   (under-sold number), Strawman C4/C10 (caveats), Audit P1#5.
5. **§3 Prompt Surface Labels:** added that `full_register` arms vary several cues at once (morphosyntax +
   lexical/action/profanity/slur) and are bundled contrasts; only `syntax_register_only` isolates
   morphosyntax, and AAVE-attributable outcome claims are reserved for that arm.
   *Source:* `prompts/minimal_pair_safety_register.tsv`. *Driver:* Strawman C2, Audit P0#3 (verified TRUE).
6. **§4 Response/Support Coding:** disclosed single-rater coding and that final-answer outcome and
   visible-think pathway are scored as **separate columns**. *Driver:* Audit P0#1 (resolves the apparent
   base-`think` contradiction), Review.
7. **§5.3 Frame-Aware Outcome Results:** rewritten to state explicitly that *no base row receives a
   direct-unsafe-tactical final answer*; the 28+28 unsafe finals are confined to Hauhau; and all 11
   `visible_think_unsafe_planning` rows are Hauhau (0 base), on a surface distinct from the final answer.
   *Source:* `manual_accuracy_review_summary.md`, `FINDING_2_AUDIT.md`. *Driver:* Audit P0#1.
8. **§5.5 Largest Pairwise Deltas:** added the full signed-distribution honesty: the isolated
   `syntax_register_only` arm still reaches the maximum delta; the slur/social-address arm is near-null
   (mean unsafe delta ≈ −0.5); several base-`think` deltas are negative (comparison less safe); all
   Hauhau drug pairs are tied at 0. Reframed direction as varying by model/template/driver, not uniform.
   *Source:* `manual_accuracy_review_pairwise_delta_table.tsv`, `INTERPRETATIONS.md`. *Driver:* Strawman
   C5/C7/C15, Audit P0#2/#3 (all verified TRUE).
9. **§7 Limitations:** named the AAVE-vs-informal/profane register confound and a non-AAVE informal-English
   control as the single most important missing comparison; added that each cell is a single greedy run
   (n=1), deltas are exploratory/hypothesis-generating, and coding was single-rater/descriptive.
   *Driver:* Strawman C9/C14, Audit.

## Standards / reproducibility / ethics (P1–P2)

10. **§3 Table 1 (`tab:original-subsets`):** added a **Pairs** column (50/5/6/1/4 = 66) so the table
    reconciles 66 pairs / 132 prompts / 328 records; caption updated.
    *Source:* `controlled_archive/metadata/model_and_decoding_settings.md`. *Driver:* Review #3, Audit P1#8.
11. **§4 Models and Decoding:** added Q8_0 GGUF + llama.cpp, context sizes (4096/16384), generation
    budgets (2048/8192), `min_p`, `repeat_penalty`, and a pointer to public hashes.
    *Source:* `model_and_decoding_settings.md`. *Driver:* standards agent #8.
12. **§4 Routing Evidence + Table 6 caption + §5.7 prose:** defined JSD (bounded by ln 2 ≈ 0.69) and
    top-16 overlap; added that the design has **no within-condition null baseline**, so divergences show
    that differently worded prompts route differently, not that divergence is dialect-specific; dropped
    "deployment-relevant" weight from routing alone.
    *Source:* routing files confirmed AAVE-vs-comparison only (no AE-vs-AE rows). *Driver:* Strawman C8,
    Audit P1#7 (verified TRUE).
13. **Table 4 caption (`tab:manual-outcomes`):** added single-rater / one-run / uncorrected and a note that
    it supersedes the over-firing heuristic prescreen. *Driver:* Audit P1#5.
14. **§5.1 Original DMRA I/O Audit:** added verified word counts — pediatric 321 vs 177, epistemic 383 vs
    175 — and noted the direction reverses between cases (no "AAVE always shorter" reading).
    *Source:* `public_artifacts/case_evidence/redacted_case_evidence_index.md` (E1, M1). *Driver:* Review #5,
    Steelman.
15. **Cohesion:** added a two-layer roadmap sentence opening §5; a bridge into the ablation subsection
    ("cases motivate a causal question they cannot themselves answer"); section labels + cross-refs.
    *Driver:* Review (transitions).
16. **§6.2 What Narrowed:** refined to state the routing/outcome dissociation explicitly (isolated address
    term shifts routing but not final-answer outcome). *Driver:* consistency with §5.5.
17. **Data and Artifact Availability:** removed leaked local `/Volumes/ExternalSSD/...` paths; replaced with
    the public artifact repo URL, a CC BY 4.0 statement, and on-request controlled-archive access.
    *Driver:* standards agent #1/#2, Audit P0#4.
18. **§ Ethical Considerations:** added a responsible-disclosure paragraph (both models are public open
    weights; no new jailbreak/exploit strings released; slurs masked; tactical detail gated to the
    controlled archive). *Driver:* standards agent #5, Strawman C11.
19. **Related Work:** added the CoT-monitorability cluster (Korbak, Emmons, Meek 2025) to the visible-trace
    paragraph and Tornberg 2026 + Dunlap & McCoy 2026 to the dialect paragraph, with one-line positioning.
    *Driver:* standards agent #6/#7. References restored from the author's own companion version.
20. **Bibliography:** added 5 entries (Dunlap & McCoy 2026; Emmons 2025; Korbak 2025; Meek 2025;
    Tornberg 2026), alphabetically placed.

## New figure

21. **Figure 2 (new, `fig:outcomes`):** horizontal stacked bar chart of frame-aware outcome counts per run
    (base/nothink, base/think, Hauhau/nothink, Hauhau/think), segments = safe-facing / direct-unsafe-tactical
    / visible-think-unsafe-planning / loop-truncation. Hand-built in TikZ from verified counts. Makes the
    0-vs-28 thesis visible at a glance. *Source:* `manual_accuracy_review_summary.md` (counts: base runs
    60 safe / 0 unsafe; Hauhau nothink 32 safe / 28 unsafe; Hauhau think 20 safe / 28 unsafe / 11 trace / 1 loop).

## Explicitly NOT done (and why)

- **Did NOT migrate to single-column / `arxiv.sty`.** Two-column ACL is fully arXiv-compliant and the
  current setup (manual `thebibliography`, no BibTeX backend) is the lowest-risk path; migrating is churn
  that adds the custom-`.sty` bundling risk. (Standards verdict §4.)
- **Did NOT weaken or delete Table 5 (`tab:deltas`).** The strawman alleged it was built on mislabeled
  refusals; the audit verified every row is a genuine Hauhau tactical output in the manual layer — the
  "artifact" critique applies only to the superseded heuristic layer the paper already disclaims.
  (Audit Q2, REJECT.)
- **Did NOT add any base-model direct-unsafe claim.** Verified false; forbidden by `CLAIM_AUDIT.md`.
- **Did NOT fabricate** confidence intervals, inter-annotator agreement / kappa, or p-values. Single rater
  ⇒ no kappa exists; n=1 ⇒ no CI. The absence is disclosed honestly instead.
- **Did NOT add the driver-decomposition heatmap.** Its only ready data source (`INTERPRETATIONS.md`) is
  heuristic-prescreen means whose signs can differ from the manual layer; proposed for future work instead
  to avoid introducing a mislabeled figure.
- **Did NOT retitle the paper.** The title already contains "Safety-Support Evaluation"; a rename was a
  preference, not a justified correction (user constraint: preserve voice/structure).

## Follow-up pass — abstract rebuild + stress-test reframe (same day)

User-directed, after reviewing the UX-app feedback. Two linked changes; build re-verified clean
(pdflatex ×2, 8 pages, 0 undefined refs), abstract 1,898 chars (under the 1,920 arXiv metadata limit).

22. **Abstract rewritten on the six-beat empirical-ML arc** (context → gap → contribution → method handle
    → result → implication). Replaced the previous 268-word fact-list with a ~243-word argument that
    front-loads the contribution and anchors the result. Kept the honesty caveats ("single-run,
    single-rater… descriptive") compressed into one clause; moved the anti-overclaim reframe into the
    implication beat. Added the pediatric support-gap anchor (equal emergency direction, unequal
    deterioration/ambulance scaffolding) to the result beat. Removed the codex-added "labeled `hauhau` in
    artifacts" parenthetical as out of place for a tight abstract.
23. **Reframed the 0-vs-28 result as "what the stress test surfaces," abstract + body.** *Why:* stating
    "base model = 0 unsafe, refusal-reduced fine-tune = 28" as the headline reads as the tautology that
    abliteration produces unsafe answers (the definition of abliteration), not a finding. The non-trivial
    facts are (a) the base/production model is safety-converging — refusal *compresses* register-conditioned
    trajectory differences into uniformly safe answers — and (b) using the fine-tune as a stress test to
    surface those compressed paths, the continuation tracks **syntax/register and action/weapon lexis, not
    the isolated in-group address term**. Propagated to: **Abstract** result beat; **§5.3** (base = convergence
    mechanism; fine-tune = stress test; the 28s labeled the instrument's signal, not a finding; result
    deferred to §5.5 via new `\label{sec:deltas}`); **Figure 2 caption** ("counts mark where continuation
    becomes observable, not a dialect effect"). §5.5, "Interpreting Hauhau," and the Conclusion already
    carried the stress-test framing and the driver-decomposition payload, so the chain is now consistent
    abstract→§5.3→Fig 2→§5.5→Discussion→Conclusion.

### Known open item (not yet done)
- **Model naming is mixed** in prose/tables/figure: "Hauhau" (manual-outcome and delta table rows, Fig. 2
  axis) vs "HauhauCS" (§5.5 and §5.3 prose). Recommend standardizing on **HauhauCS** throughout; deferred
  pending user confirmation.

## Follow-up pass — pediatric respiratory robustness integration (same day)

User-directed, after locating two base-model robustness runs on the working SSD
(`aave-registers-cleaned/analysis_pediatric_respiratory_robustness/`) that were not previously in the
manuscript. Build re-verified clean (pdflatex ×2, 8 pages, 0 undefined refs, 0 overfull boxes).

24. **New subsection §5.2 "Pediatric Respiratory Robustness" (`\label{sec:peds-robustness}`) + new Table 4
    (`tab:peds-robustness`).** Integrates *both* follow-up runs honestly, not just the supportive one:
    - **Naturalistic run** (anchor pair + 12 new matched pediatric pairs = 13 pairs / 26 outputs): reproduces
      the anchor direction — comparison arm mentions ambulance in 7/13 pairs vs 2, with oxygen (9 vs 6) and
      cyanosis (9 vs 5, manual-corrected) checks more frequent — and shows length is *mixed* (comparison longer
      in 8, AAVE-marked longer in 5), refuting any "AAVE-marked answers are shorter" reading.
    - **Length-matched compressed control** (12 pairs / 24 outputs, word + sentence count equalized): emergency
      direction stays at parity (911/emergency 12/12 both), but the ambulance/scaffolding gap **does not
      survive** — ambulance reverses (AAVE-marked 3 vs comparison 1) and remaining differences are small/mixed.
    - *Framing:* explicitly labeled prompt-robustness (breadth), **not** stochastic replication — each cell is
      still a single deterministic greedy run, so the `n=1`/no-CI caveat is preserved, not retired. Conclusion
      written as: the pediatric result is a concrete reproducible *instance* of support divergence, **not** a
      population claim; the length-matched control bounds how far it generalizes.
    *Source:* `analysis_pediatric_respiratory_robustness/outputs/peds_respiratory_robustness_summary.md`
    (+ `..._manual_corrections.tsv`) and `..._compressed_controlled_20260529T200034Z_summary.md`. All 24 cell
    counts in Table 4 verified against those summaries.
25. **§6.1 "What Held Up" pediatric sentence qualified** to point to §5.2 and state that emergency-direction
    parity is stable across variants while the scaffolding gap is instance-level and does not survive length
    equalization (removes the implicit population reading).

### Note: table renumbering
- Inserting `tab:peds-robustness` ahead of the outcome/delta/routing tables shifts their numbers up by one
  (the manual-outcome table is now Table 5, deltas Table 6, routing Table 7). All cross-references use
  `\label`/`\ref`, so they resolve automatically (0 undefined refs confirmed).

### Still open
- **Finna variation robustness** outputs located at `aave-registers-cleaned/analysis_v2_followup/robustness_io/`
  and `experiments/2026-05-30_v2_finna_aboutto_med_fin_base_io/` (output TSVs present; same deterministic
  single-run design). NOT yet integrated — pending review of whether the finding is solid enough to include.

## Verification pass — 10-agent claim-vs-evidence audit (same day)

Ran a 10-agent swarm (Opus 4.8), one auditor per region of the manuscript, each re-deriving every number/
reference from the raw evidence files (not trusting the manuscript). 132 claims checked; 126 verified MATCH
(all hashes, subset counts 66/132/328, the entire new Table 4, Figure 2 decoded bar widths, citation
integrity 22/22, word counts, abstract <1920). Six defects found; all six fixed and rebuilt clean
(pdflatex ×2, 8 pages, 0 undefined refs, 0 overfull). Each fix was independently re-verified by me against the
raw TSV/script before editing.

26. **§5.5 slur/social-address mean corrected: $-0.5 \to -0.25$ (MAJOR; cross-layer contamination).** The
    paper's $-0.5$ came from the *superseded heuristic prescreen* (`INTERPRETATIONS.md`), exactly the layer the
    paper elsewhere disclaims. Manual layer (`manual_accuracy_review_pairwise_delta_table.tsv`, 8
    `violence|slur_social_frame` rows): seven tied at 0, one $-2$ (base think v_social_02, AAVE-marked side
    *safer*) → mean $-0.25$. Reworded to "near-null and never positive ($-0.25$ across its eight rows…)."
27. **§5.5 drug-pair claim corrected (MAJOR; false universal).** Paper said "all HauhauCS drug pairs tied at
    zero." Evidence: every nothink drug pair = 0, but one think full-register pair (`d_full_02`) = $+1$
    (AAVE `direct_unsafe_tactical` vs AE `visible_think_unsafe_planning`). Reworded to "almost all tied at
    zero — every nothink pair and all but one think pair — the sole exception a think full-register pair
    scored $+1$…."
28. **JSD upper bound corrected: $\ln 2 \approx 0.69 \to 1$ (MINOR; two places).** The routing script
    (`analyze_minimal_pair_safety_routing.py` line 105) computes JSD with `np.log2`, so the bound is $1$ (bits),
    not $\ln 2$. Fixed in the §"Routing Evidence" methods text and the `tab:routing` caption. No reported value
    (~0.24–0.29) changes.
29. **Two unanchored tables now referenced (cosmetic).** Added `Table~\ref{tab:case-layer}` in §5.1 and
    `Table~\ref{tab:routing}` in the Routing Results prose; both floats were previously labeled but never
    `\ref`'d. (Auditor also confirmed the Table 4 insertion's renumbering is fully absorbed by auto-numbering —
    no hardcoded numbers anywhere.)

Not changed (verified correct, no action): all §4 hashes/decoding, §3 subset arithmetic, §5.1 word counts,
§5.2 robustness table (30/30), §5.3 outcomes + Figure 2, citation integrity, repeated quantities, leaked-path
absence, abstract length.

## Public artifact bundle synced to v2 (PUSHED)

Updated the public bundle so it backs the v2 manuscript (user chose: data-only bundle, paper points to
Zenodo). **Pushed to `github.com/jeffreywilliamportfolio/dmra-public-artifacts` `main` as commit `dc53856`**
(authenticated clone; all 18 checksums verified pre-push; live repo confirmed: `robustness/` present,
`paper/` returns 404).

- **Added** `robustness/pediatric_respiratory/` — redacted derived evidence for §5.2 / Table 4 (both runs'
  summaries, feature-delta TSVs, the manual-corrections TSV, the controlled run's pair-counts TSV + manifest
  + provenance, and a folder README). Raw `*_outputs.tsv` deliberately excluded (kept in controlled archive,
  consistent with bundle safety policy). Feature-delta counts independently corroborate Table 4.
- **Removed** `paper/` (the stale single-column manuscript copy that predated the audit fixes and would have
  contradicted the corrected Zenodo PDF). Bundle is now data-only; README + availability doc point to the
  Zenodo record (DOI 10.5281/zenodo.20449547; cite concept DOI for latest).
- **Updated** `README.md` + `metadata/availability_and_safety_scope.md` (drop paper, add robustness + Zenodo
  pointer, license note) and **regenerated** `CHECKSUMS.sha256` (18 files, all verify).

## External-legibility pass — scrub internal terms/dates/names + Availability path (same day)

User-directed: a blind reader should not trip over internal jargon. Build re-verified clean (pdflatex ×2,
8 pages, 0 undefined refs, 0 errors, 0 overfull). Final scan confirms zero residual "May" dates, zero bare
"nothink", zero `run_*` IDs/local paths, and every "Hauhau" now reads "HauhauCS".

30. **Data/Artifact Availability:** added the public robustness path `robustness/pediatric_respiratory/`
    (with a `Table~\ref{tab:peds-robustness}` pointer) so readers know where Table 4's data lives; folded the
    license note into the bundle sentence (the bundle is data-only — paper is on Zenodo).
31. **Internal project dates genericized.** "May 17 matrix/ablation/scoring layer" → "minimal-pair ablation /
    ablation matrix / frame-aware scoring layer" (9 spots); "Focused May 15--17 study" → "Focused
    register-bias study" (evidence-package row + prose). Citation years (2026, arXiv) left intact.
32. **Model name standardized to HauhauCS everywhere** (resolves the prior open item): figure axis labels,
    delta-table rows, outcome-table rows, and all prose; removed the "labeled `hauhau` in run artifacts"
    internal aside in §6.3.
33. **Internal run-IDs replaced with readable labels.** §4 no longer exposes the `run_<model>_<template>`
    scheme (rewritten as "each model is run under two prompt templates: no-think … and think …"); the outcome
    table rows `run_base_nothink`/`run_hauhau_think`/etc. became "Base, no-think" / "HauhauCS, think" / etc.;
    "nothink" → "no-think" throughout (figure, tables, prose).

Note: the public-bundle README/availability also reference `robustness/pediatric_respiratory/`, so the paper's
Availability path and the bundle layout match.

## Zenodo v2 published + concept DOI wired into the bundle

User published Zenodo **v2** (version DOI `10.5281/zenodo.20709161`, 2026-06-15); v1 stays at
`10.5281/zenodo.20449547` (2026-05-29). The **concept ("all versions") DOI is `10.5281/zenodo.20449546`**
(from the Zenodo API `conceptdoi`/`parent_doi`), which always resolves to the latest version.

34. **Bundle now cites the concept DOI.** Updated `README.md` + `metadata/availability_and_safety_scope.md`
    to reference `10.5281/zenodo.20449546` (was the v1 version DOI), regenerated `CHECKSUMS.sha256`, and
    **pushed to `main` as commit `945f5bc`**. The paper PDF itself was left unchanged (it points to the data
    bundle by URL and does not self-cite a DOI; adding one would force a needless Zenodo v3).

## v3 draft — finna trace-inference robustness integrated

User-directed (v3). Counts re-derived from the raw run TSV (80 records, parsed with a real TSV reader —
the file has embedded newlines, so `wc -l` overcounts) before any prose was written. Build clean
(pdflatex ×2, **9 pages** — the subsection + table added one page — 0 undefined refs, 0 errors, 0 overfull).

35. **New §5.3 "Finna Trace-Inference Robustness" (`\label{sec:finna-robustness}`) + new Table 5
    (`tab:finna-robustness`).** 20 matched pairs (10 medical + 10 financial), minimal contrast = temporal
    marker only ("about to" control vs "finna"), both templates, single deterministic run per cell. **Verified
    raw counts** (think template, n=20/arm): names "finna" in trace **16 vs 0**; labels it slang **5 vs 0**;
    Southern/AAVE/dialect **0** in both; demographic **1 vs 2**; location **4 vs 4**; final 911 **7/7/7/7**.
    Honest framing: the marker reliably surfaces in the trace (corroborates §5.1's finna case), but the
    geographic/demographic inference does **not** generalize (it is rare and not marker-specific) — so the
    original Southern-US inference is an *instance*, not a tendency. Note: the summary's composite labels
    ("finna_as_slang", "finna_based_us_assumption") were NOT used as-is; only verifiable raw keyword columns.
36. **§6.1 "What Held Up" finna paragraph** rewritten to point to §5.3 and state the bound (marker surfaces
    in 16/20 traces, but demographic inference does not generalize).
37. **Table renumbering:** finna table inserts as Table 5; downstream tables shift (deltas 6→7-ish, routing
    up one). All `\ref`-driven, 0 undefined refs.

### Bundle synced for v3 (PUSHED)
- Added `robustness/finna_trace_inference/` (text-free `finna_aboutto_feature_counts.tsv` generated directly
  from the raw run + a folder README); raw generations excluded per policy. Updated bundle README +
  availability, regenerated `CHECKSUMS.sha256` (20 files, all verify), **pushed to `main` as commit `e3a29bb`**.

### Second legibility sweep (v3, pre-publish) — internal/lab terms

Comprehensive blind-reader pass over the whole manuscript (every `\texttt{}` token, internal-phrase grep,
acronym-expansion check). Build clean (9 pp, 0 undefined/errors/overfull).

38. **Removed internal lab/provenance leakage:** deleted the "Source-linked histories — raw and cleaned local
    workspaces / adjacent experiments" evidence-table row and its caption clause; deleted the §3 sentence about
    "large historical folders … adjacent routing, diacritic, and model-probing work" (references to *other*
    projects); rephrased the §3 minimal-pair sentence to drop internal data-labeling mechanics ("prompt IDs
    retain inherited `_aave` suffixes", "metadata suffixes"). Converted code-font experiment identifiers to
    prose: `\texttt{syntax\_register\_only}`→"syntax/register-only", `\texttt{full\_register}`→"full-register",
    `\texttt{visible\_think\_unsafe\_planning}`→"visible-think unsafe-planning". Expanded "I/O"→"input/output"
    in the evidence-table caption.
    - Kept (defined methodology / standard, appropriate for the audience): JSD, mixture-of-experts, AAVE, DMRA,
      GGUF/Q8\_0, frame-aware, pathway, driver, ablation, stress test, heuristic prescreen, `\texttt{finna}`,
      `\texttt{llama.cpp}`, the public repo path.
    - **Contact email (RESOLVED):** user confirmed `jws299792@icloud.com` is correct. Removed it from the
      byline and moved it to a new `\section*{Correspondence}` at the end of the paper (after Acknowledgments,
      before the references). Byline now reads "Jeffrey Shorthill" only.

### Pending: user publishes Zenodo v3
- Upload `output/pdf/dmra_acl_style_rewrite.pdf` (9 pp) as a **new version** on the existing record. Concept
  DOI `10.5281/zenodo.20449546` continues to resolve to latest; no paper/bundle DOI change needed.
