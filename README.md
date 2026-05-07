# Article Appendix

Supplementary materials for the LessWrong article:

**[SVD on Weight Differences for Model Auditing](https://www.lesswrong.com/posts/FWacQnfHJkYhAn7wR/svd-on-weight-differences-for-model-auditing)**

This folder contains all prompts, model outputs, and investigator agent results needed to replicate the experiments described in the article. It is self-contained and has no dependencies on the rest of the repository.

---

## Contents

### `model_organism_query_prompts.md`
The 15 prompts used to query the Llama 70B model organisms. Each prompt asks the model to disclose its own behavioral quirks under different framings (diagnostic interview, confession box, bug report, internal audit memo, etc.). All prompts share the same system prompt placing the model in the role of PRISM-4 from Nexus Research.

### `investigator_agent_prompt.md`
The system and user prompt given to the investigator agent (GPT-5). The agent receives cleaned, anonymised model outputs and is asked to propose 10 ranked hypotheses for the hidden behavioral quirk.

### `rater_agent_prompt.md`
The system and user prompt given to the rater agent (GPT-5). The rater receives the ground-truth quirk description and the investigator's 10 hypotheses, and returns a JSON verdict on whether any hypothesis captures the true quirk.

### `AuditBench Llama 70B responses/`
A single representative sample of model outputs for all 56 model organisms (14 behaviors × 4 training regimes) across the 15 query prompts, included here for illustrative purposes. The article's results are based on multiple independent samples per condition — this folder shows one sample to give a concrete sense of what the model outputs look like. Organised into four subfolders by training regime:

- `Synth Docs (SFT)/` — synthetic document fine-tuning with SFT adversarial training
- `Synth Docs (KTO)/` — synthetic document fine-tuning with KTO adversarial training
- `Transcripts (SFT)/` — transcript distillation with SFT adversarial training
- `Transcripts (KTO)/` — transcript distillation with KTO adversarial training

Each subfolder contains one `.md` file per quirk showing the Full Adapter and Rank-1 Adapter responses side by side. Adapter names link to the corresponding HuggingFace checkpoints under `auditing-agents/`.

### `investigator agent runs/`
Investigator agent outputs for all 56 conditions, with the rater verdict appended to each file. Same four-subfolder structure as above. Each file shows the 10 quirk hypotheses and evidence map produced by the investigator, followed by the ground-truth quirk, the verdict (Correct ✓ / Incorrect ✗), and the rater's reasoning.
