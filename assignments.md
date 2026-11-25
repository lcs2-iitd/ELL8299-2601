---
layout: assignments
title: Assignments
permalink: /assignments/
---

Two programming assignments, each worth **75 marks** and **10%** of the course grade. Both are built on small open models (Qwen2.5, 0.5B to 1.5B) with data provided by the course, and are submitted on Moodle with code and a short report.

## Assignment 1: Fine-Tune, Sanitize, Extract

**Deadline:** September 14, 2026, 05:00 PM IST · [Download PDF]({{ site.baseurl }}/static_files/pdfs/A1.pdf)

An end-to-end look at how private information ends up in fine-tuned models, and how far sanitization goes in preventing it.

- **Part A, PEFT (25 marks):** fine-tune a PII sanitizer with LoRA and QLoRA, comparing adapter placement, rank and scaling against accuracy, memory and time.
- **Part B, Sanitizer evaluation (25 marks):** measure entity-level precision, recall and F1, leak rate and over-masking against rule-based and zero-shot baselines, including out-of-distribution data.
- **Part C, Extraction attacks (25 marks):** attack victim models trained on raw and sanitized corpora (discoverable memorization, untargeted extraction, canary exposure) and quantify the privacy-utility trade-off.

## Assignment 2: Debias, Watermark, Abstain

**Deadline:** November 5, 2026, 11:59 PM IST · [Download PDF]({{ site.baseurl }}/static_files/pdfs/A2.pdf)

Three components that make a small LLM more trustworthy, one per course module, each evaluated on a private test set.

- **Task 1, Bias and Fairness (25 marks):** a question-answering system that answers from the evidence, chooses "unknown" when the context does not say, and stays accurate on general questions.
- **Task 2, Watermarking (25 marks):** a watermarked text generator and a detector that scores a text with no access to the prompt.
- **Task 3, Uncertainty (25 marks):** a QA system that reports calibrated confidence and abstains when it is likely to be wrong.
