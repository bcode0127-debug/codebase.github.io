---
layout: page
title: Genome Firewall
description: Calibrated antibiotic-resistance prediction with confidence, named evidence, and an explicit no-call when the evidence does not support an answer
importance: 1
category: Hackathon
github: https://github.com/bcode0127-debug/genome-firewall
related_publications: false
---

Predicts which antibiotics will fail against a *Klebsiella pneumoniae* genome days before laboratory results arrive, with calibrated confidence, named supporting genes, and an explicit no-call when the evidence is insufficient. Built for Hack-Nation's 6th Global AI Hackathon (Challenge 06, OpenAI).

**Live app:** [genome-firewall on Streamlit](https://genome-firewall-lln2cdi8zxqy8pnfuinfen.streamlit.app)

## What it does

FASTA → AMRFinderPlus → gene-presence features → one calibrated model per drug → verdict, confidence, evidence category, or a no-call. Three drugs: meropenem, ceftazidime, gentamicin.

## Results (held-out test set, clone ST258 never seen in training)

| Metric | Meropenem | Ceftazidime | Gentamicin |
| :--- | :---: | :---: | :---: |
| Balanced accuracy | 0.926 | 0.899 | 0.825 |
| AUROC | 0.944 | 0.947 | 0.875 |
| Brier | 0.081 | 0.060 | 0.115 |
| No-call rate | 4.2% | 4.1% | 28.9% |
| Conformal coverage | 0.897 | 0.901 | 0.891 |
{: .table .table-sm .table-borderless}

## What didn't hold up

The distinguishing part: I measured my own safety mechanisms and published the shortfalls rather than hiding them.

- **Conformal coverage on gentamicin** reached 72.4% against a nominal 90%. Tightening alpha reached 89.1%, still short, at the cost of abstaining on 28.9% of cases.
- **The novelty gate** raises observed error 6.7% → 14.8% on meropenem and 13.7% → 21.3% on gentamicin, but shows no discrimination on ceftazidime, so it ships advisory-only.
- **Mash validation of the MLST split** found a limitation: ST437 sits in training at distance 0.0034 from held-out ST258, closer than some same-clone pairs.

## Limitations

One species, three of 74 antibiotics, gene presence/absence only. A research prototype: every result requires confirmation by standard laboratory testing. Genomic phenotype data from BV-BRC; resistance-gene annotation via NCBI AMRFinderPlus; genome-distance validation via Mash.
