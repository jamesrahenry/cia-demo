# CIA Sentinel Demo

> *What is the model thinking about, regardless of what it ends up saying?*

This repo contains demo materials for the **Concept Integrity Auditor (CIA)** — a mechanistic interpretability tool that monitors which security-relevant concepts an LLM engages with internally during a forward pass, and emits events when they activate.

## Live demo

| Service | URL |
|---------|-----|
| CIA Sentinel API | http://cia-demo.henrynet.ca:8000/docs |
| A/B demo UI | http://cia-demo.henrynet.ca:8501 |
| JupyterLab | http://cia-demo.henrynet.ca:8888 |

## What's in this repo

| Path | Description |
|------|-------------|
| [`notebooks/01_caz_science.ipynb`](notebooks/01_caz_science.ipynb) | The science: how concept geometry emerges in residual streams (CAZ framework) |
| [`notebooks/02_cia_demo.ipynb`](notebooks/02_cia_demo.ipynb) | Driving the CIA API from a notebook — live concept scores, audit log |

## The science in 60 seconds

Large language models encode abstract concepts as geometric structures in their residual streams — long before those concepts appear in the output. The **Concept Allocation Zone (CAZ)** framework localises where a concept crystallises layer by layer: a separation peak that is reproducible across model families, architectures, and scales.

The CIA instruments a model with forward hooks and reads those peaks in real time. One forward pass produces both the text response and a concept engagement report.

```
Input text
  └── CIA (transformers + residual stream hooks)
        ├── text response   →  normal LLM output
        └── /v1/audit       →  {"exfiltration": 0.74, "obfuscation": 0.53, ...}
```

No training. No fine-tuning. No model modification. If you have the weights, you can run the CIA.

## Concepts monitored

| Concept | Security role |
|---------|---------------|
| `exfiltration` | Data movement intent |
| `obfuscation` | Concealment of intent |
| `authorization` | Access control framing |
| `deceptive_intent` | Output-level misdirection |
| `threat_severity` | Triage signal accuracy |
| `urgency` | Pressure and manipulation detection |
| `negation` | Policy bypass framing |
| `source_credibility` | Social engineering resistance |
| `causation` | Attribution chains |

## Related repos

| Repo | Description |
|------|-------------|
| [VectorInstitute/Concept_Integrity_Auditor](https://github.com/VectorInstitute/Concept_Integrity_Auditor) | CIA source code (public) |
| [jamesrahenry/Rosetta](https://github.com/jamesrahenry/Rosetta) | CAZ framework notebooks and paper companions |
| [jamesrahenry/Rosetta_Concept_Pairs](https://github.com/jamesrahenry/Rosetta_Concept_Pairs) | Contrastive concept pair dataset used for probe training |
| [jamesrahenry/rosetta_tools](https://github.com/jamesrahenry/rosetta_tools) | Python library: CAZ extraction, GEM, PRH alignment |

## Research

The CAZ framework underlying the CIA is described in:

- Henry, J. (2026a). *Concept Allocation Zones: Layer-wise concept formation in transformer residual streams.* arXiv:2605.24856 — CAZ framework
- Henry, J. (2026b). *Geometric Evolution Maps: Layer-resolved concept assembly in large language models.* arXiv:2605.25848 — GEM / residual stream assembly
