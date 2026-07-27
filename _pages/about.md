---
layout: about
title: About
permalink: /
subtitle: ML Engineer | Mechanistic Interpretability & AI Safety
profile:
  align: right
  image: Prof_pic2.jpg
  image_circular: true
  selected_papers: false
  social: true
announcements:
  enabled: false
  scrollable: true
  limit: 5
latest_posts:
  enabled: false
  scrollable: true
  limit: 3
---

I'm an ML engineer transitioning toward mechanistic interpretability research, grounded in independent work reverse-engineering Transformer and LSTM failure modes via layer-wise attention analysis. My production ML background across fraud modeling and real-time streaming infrastructure brings engineering rigor (falsifiable hypotheses, controlled experiments, ground-truth eval harnesses) to interpretability research.

**Current Research:** My independent project, _Neural Sequence Models: Compositional Reasoning_, investigates why LSTM and Transformer encoder-decoders fail to generalize on out-of-distribution arithmetic despite high in-distribution accuracy. An early version produced clean-looking results until I found an input-truncation bug that had corrupted 99% of the OOD evaluation set, invalidating them; I rebuilt the datasets and re-ran a 12-seed matrix. The corrected findings: a 2.6x-larger Transformer memorizes training data to 98% but generalizes at only 7.3%, failing at the first decoding step 71% of the time, evidence it learned answer format without performing the computation, while the LSTM degrades more gracefully to 35.7% held-out accuracy.

I also built _Pipeline Pathologist_ for the GitLab Duo Hackathon, research tooling that uses semantic call-graph traversal to diagnose CI/CD pipeline failures with a verifiable evidence chain instead of a raw log dump. It has three explicit guards against false attribution (flaky guard, honesty guard, multi-hop disambiguation), achieving 5/5 on a five-class ground-truth eval harness in under 5ms on a 64-node graph. [Watch the demo video](https://www.youtube.com/watch?v=KP65jnzNT5U).

I also built _Genome Firewall_ for Hack-Nation's Global AI Hackathon (OpenAI challenge): a calibrated model that predicts antibiotic resistance from a bacterial genome with confidence, named supporting genes, and an explicit no-call when the evidence is insufficient (0.93/0.90/0.83 balanced accuracy across three drugs, with conformal prediction). In keeping with how I think about evaluation, I measured the system's own safety mechanisms and published where they fell short rather than hiding them. [Live app](https://genome-firewall-lln2cdi8zxqy8pnfuinfen.streamlit.app).

**Applied Experience:** At SageNet, I engineered the end-to-end real-time streaming pipeline serving 430K+ distributed enterprise network endpoints, including multi-tenant Kafka ingestion, Isolation Forest-based anomaly scoring, and a containerized ML scoring microservice with p95 alert-to-ticket latency under 30 seconds. I also architected a multi-agent LLM triage system on the live ticket stream, using a RAG pipeline that grounded incident classification in historical runbooks and resolved-ticket embeddings, with specialist agents for severity classification, root-cause hypothesis, and routing. At Bank of America, I built the training-serving parity framework and SR 11-7 model governance engine, and delivered a challenger fraud model (AUC 0.94-0.96) that captured 8-10% more fraud value at equal alert volume with 15-20% fewer false declines.

This engineering background shapes how I approach interpretability: as an empirical discipline that demands the same rigor as production ML, with falsifiable hypotheses, controlled experiments, and ground-truth eval harnesses.

#### **Research Interests & Open To**

**Research Areas**

- Mechanistic Interpretability and Attention Circuit Analysis
- Compositional Generalization and Out-of-Distribution Robustness
- Controlled Experiment Design and Eval Harness Design
- Falsifiable Hypothesis Testing for Neural Network Failure Analysis

**Open to Collaborate On**

- Mechanistic Interpretability Tools and Research Tooling
- AI Safety and Model Evaluation
- Agentic AI Systems and CI/CD Diagnostic Tooling
- Production ML Systems Engineering at Scale

**Actively Seeking**

- Research Scientist and ML Research Engineer roles focused on mechanistic interpretability
- Positions combining interpretability research with production ML systems engineering
- Opportunities to contribute to foundational research on neural network robustness
- Contract or full-time roles at AI safety-focused labs
