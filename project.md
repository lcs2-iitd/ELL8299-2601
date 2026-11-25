---
layout: page
title: Project
permalink: /project/
---

The course project is exploratory research done in **groups of up to 2** and carries **25%** of the course grade, the largest single component. Four problem statements were floated, each with a consulting TA; groups could also propose their own topic with the instructors' approval.

- **Submission deadline:** November 29, 2026, by midnight.
- **Presentations:** November 30, 2026, 9 AM to 2 PM. Slots have been emailed to the groups.
- **Submission:** a GitHub repository with the complete source code, and a report in the [ACL format](https://www.overleaf.com/latex/templates/association-for-computational-linguistics-acl-conference/jvxskxpnznfj).
- **Evaluation:** rigor of experiments and analysis. Negative results are welcome when their causes are analyzed and reported transparently.
- **Integrity:** no plagiarism and no GenAI-written reports. Public code may be reused if cited.

## 1. How Secure is Your Specialized Knowledge?

**Weight-stealing attacks and defenses in multi-agent LLM systems** · Consulting TA: [Prottay Kumar Adhikary](https://proadhikary.github.io)

Two small language model agents share a simulated file system. The Victim is LoRA fine-tuned on specialized text; the Attacker tries to gain that knowledge not by conversation, but by locating and copying the Victim's adapter weights and merging them into its own model.

- **Setup:** two [Llama-3.2-1B](https://huggingface.co/meta-llama/Llama-3.2-1B) agents built with LangChain; the Attacker has Python/shell tools to explore the shared directory.
- **Attack:** find and copy the [LoRA](https://huggingface.co/docs/peft/main/conceptual_guides/lora) adapter files, then integrate them with a [merging technique](https://huggingface.co/docs/peft/en/developer_guides/model_merging) such as TIES-Merging.
- **Evaluation:** performance gain of the merged Attacker over its baseline on the Victim's domain.
- **Deliverables:** code, model weights on Hugging Face, and a report covering the attack strategy, quantitative results, and defenses such as file permissions and agent sandboxing.
- **Background:** [Stealing Machine Learning Models via Prediction APIs](https://www.usenix.org/conference/usenixsecurity16/technical-sessions/presentation/tramer) (Tramèr et al., 2016).

## 2. Who Wrote this Code?

**Pushing the limits of code watermarking** · Consulting TA: [T Karthikeyan](https://tkarthikeyan132.github.io)

Build a watermark for LLM-generated code that is statistically detectable, keeps the code compiling and passing its tests, and survives reformatting, variable renaming and minor refactoring. Standard Green-Red watermarking breaks on code: syntax leaves few valid next tokens, so a random vocabulary split can force a syntax error or weaken the signal.

- **Directions:** add a refactoring-robustness reward to CodeTracer's training; partition only interchangeable tokens using type checkers or grammar states; replace unit tests with static-analysis signals.
- **Starting point:** reproduce [CodeTracer](https://github.com/TimeLovercc/CodeTracer) as the baseline, with [OpenCoder-1.5B-Instruct](https://huggingface.co/infly/OpenCoder-1.5B-Instruct) or [Qwen2.5-Coder-1.5B-Instruct](https://huggingface.co/Qwen/Qwen2.5-1.5B-Instruct).
- **Data:** train on [MBPP](https://huggingface.co/datasets/google-research-datasets/mbpp); evaluate on [HumanEval](https://huggingface.co/datasets/openai/openai_humaneval), MBPP-Test and [HumanEvalPack](https://huggingface.co/datasets/bigcode/humanevalpack).
- **Metrics:** pass rate and syntax error rate; z-score and AUROC for detection, before and after auto-formatting, identifier renaming, comment stripping and LLM paraphrasing.
- **Deliverables:** code with reproducible evaluation scripts, trained policy checkpoints, and a research write-up with ablations.
- **References:** [CodeTracer](https://openreview.net/pdf?id=4xjq3iR4aK) (Guo et al., 2026), [ACW](https://openreview.net/pdf?id=RpE4HeuX69) (Guo et al., 2025), [SWEET](https://aclanthology.org/2024.acl-long.268/) (Lee et al., 2024), [Green-Red watermark](https://icml.cc/virtual/2023/oral/25524) (Kirchenbauer et al., 2023).

## 3. Bias & Memorization Transfer: AR vs. Diffusion LLMs

Consulting TA: [Vinay Kumar](https://iitachii.netlify.app/)

Training-data memorization and social bias are well established for autoregressive (AR) LLMs. Do they also occur in diffusion language models (dLLMs), and do mitigations designed for AR models still work when the objective changes from next-token prediction to iterative denoising?

- **Models:** LLaDA-8B-Instruct vs. Llama-3-8B-Instruct, and Dream-7B-Instruct vs. Qwen2.5-7B-Instruct (matched-scale diffusion and AR pairs).
- **Bias:** BOLD, StereoSet, CrowS-Pairs and BBQ, measuring stereotype scores and demographic disparity in generations.
- **Memorization:** fine-tune on Enron Emails and measure membership-inference AUROC, exposure and verbatim extraction; validate the pipeline on [MIMIR](https://huggingface.co/datasets/iamgroot42/mimir).
- **Mitigation transfer:** deduplication, [Goldfish loss](https://arxiv.org/pdf/2406.10209) and DP-SGD, compared on privacy gain against utility retained.
- **Deliverables:** a reproducible codebase, comparison tables and plots across all four models, and a report diagnosing why the two model families differ.
- **Further reading:** [MIAs on discrete diffusion language models](https://arxiv.org/pdf/2605.16445), [Undesirable Memorization in LLMs: A Survey](https://arxiv.org/pdf/2410.02650).

## 4. Beyond Linear Directions

**Discovering and steering concept manifolds in LLMs** · Consulting TA: [Sudipto Ghosh](https://sudipto.ghosh.pro/)

Interpretability usually assumes each concept is a single direction in activation space, but many concepts form curved, low-dimensional manifolds: days of the week lie on a circle, temperature on a curve, colors on a paraboloid. Standard sparse autoencoders (SAEs) shatter or dilute these into many 1D features, and steering a single feature pushes activations off the manifold. The project is to discover, causally validate and steer such manifolds reliably.

- **Directions:** block-sparse featurizers for language models; manifold-preserving activation patching; circuit tracing between concept subspaces; unsupervised discovery of safety-relevant manifolds with Ising models.
- **Starting point:** [sae-manifold](https://github.com/goodfire-ai/sae-manifold), [block-sparse-featurizer](https://github.com/goodfire-ai/block-sparse-featurizer), [TransformerLens](https://transformerlensorg.github.io/TransformerLens/) and [SAELens](https://github.com/decoderesearch/SAELens), on [Gemma-2-2B](https://huggingface.co/google/gemma-2-2b) or [Llama-3.2-1B](https://huggingface.co/meta-llama/Llama-3.2-1B).
- **Metrics:** subspace capture, feature tiling and organization, causal steering against off-manifold degradation, and circuit faithfulness.
- **Deliverables:** modular PyTorch code, reproducible notebooks, and a report including a section on what would falsify the explanation.
- **References:** [Engels et al., 2024](https://arxiv.org/abs/2405.14860), [Zhang & Nanda, 2024](https://arxiv.org/abs/2309.16042), [Ameisen et al., 2025](https://transformer-circuits.pub/2025/attribution-graphs/methods.html), [Wu et al., 2025](https://arxiv.org/abs/2501.17148).
