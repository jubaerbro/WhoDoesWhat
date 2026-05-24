# WhoDoesWhat
# Repository Description (Short GitHub Description)

Benchmarking and improving semantic role understanding in vision-language models through relational contrastive evaluation and preference optimization.

---

# README.md

# Who Does What to Whom?

### Evaluating and Improving Semantic Role Understanding in Vision-Language Models

## Overview

Recent Vision-Language Models (VLMs) achieve impressive performance on image-caption retrieval and multimodal reasoning benchmarks. However, strong benchmark scores do not necessarily imply true relational understanding. Many models rely heavily on shallow lexical matching, object co-occurrence, or dataset priors rather than correctly understanding interactions between entities.

A critical but underexplored failure mode is **semantic role misbinding** — situations where a model recognizes the entities and actions present in an image but fails to determine **who is doing what to whom**.

For example:

* *“A dog chasing a boy”*
  vs.
* *“A boy chasing a dog”*

Both captions contain identical objects and actions, yet represent entirely different relationships.

This repository introduces a controlled benchmark and lightweight training framework designed to evaluate and improve relational reasoning in modern VLMs.

---

## Key Contributions

### 1. Relational Benchmark for VLMs

We construct a hard-negative evaluation benchmark that measures relational understanding across three dimensions:

* **Spatial Sensitivity**
  Tests whether models understand spatial relations such as:

  * left/right
  * above/below
  * in front of/behind

* **Role Sensitivity**
  Tests semantic role assignment:

  * agent vs. recipient
  * subject vs. object
  * action directionality

* **Compositional Robustness**
  Combines both spatial reversal and role swapping to create more difficult relational perturbations.

Each image is paired with:

* 1 correct caption
* 3 relationally altered hard negatives

This setup isolates genuine relational reasoning from simple keyword matching.

---

## Example

| Image Caption Type | Example                                                              |
| ------------------ | -------------------------------------------------------------------- |
| Correct            | “A man holding a cat.”                                               |
| Role Swap          | “A cat holding a man.”                                               |
| Spatial Reversal   | “A man standing behind a car.” → “A man standing in front of a car.” |
| Mixed Perturbation | Combination of both modifications                                    |

---

## RC-DPO: Relational Contrastive Direct Preference Optimization

To improve relational understanding, we introduce:

### **RC-DPO**

(Relational Contrastive Direct Preference Optimization)

RC-DPO is a lightweight post-training objective that teaches models to:

* rank relationally correct captions higher
* distinguish subtle relational differences
* increase sensitivity to semantic role structure
* reduce shallow lexical shortcut learning

The method is implemented efficiently using:

* LoRA fine-tuning
* preference optimization
* relational hard negatives

without requiring full model retraining.

---

## Experimental Findings

Our experiments reveal that current VLMs:

* perform reasonably well on simple spatial understanding
* struggle significantly with semantic role binding
* fail more severely under combined relational perturbations

After applying RC-DPO:

* relational discrimination improves substantially
* decision margins become sharper
* attention shifts toward relationally informative tokens
* global embedding geometry remains stable

---

## Supported Models

Currently evaluated on:

* Qwen2.5-VL-3B-Instruct

The framework can be extended to:

* LLaVA
* InternVL
* MiniCPM-V
* BLIP-2
* other open-source VLMs

---



## Evaluation Metrics

We evaluate models using:

* Retrieval Accuracy
* Relational Contrast Accuracy
* Margin Analysis
* Attention Sensitivity
* Robustness under Perturbation

---

## Motivation

Current multimodal benchmarks often overestimate model reasoning capabilities because they allow models to succeed through:

* object recognition
* language priors
* co-occurrence statistics

This work focuses specifically on:

> whether a model truly understands relationships between entities.

Understanding *who does what to whom* is fundamental for:

* trustworthy multimodal AI
* medical reasoning
* robotics
* autonomous systems
* human-AI interaction

---

## Future Directions

Potential extensions include:

* temporal reasoning
* multi-agent interactions
* causal understanding
* video-language reasoning
* medical vision-language evaluation
* multilingual relational reasoning

---

## Citation

