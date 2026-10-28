# [GRACE: Graph-Grounded Reflective Agent Copilot Engine for Expert-in-the-Loop Knowledge Expansion (AKBC workshop @ EMNLP 2026)](https://aclanthology.org/2026.akbc-1.16.pdf)

Builds on the code of [Graph-based Uncertainty Metrics for Long-form Language Model Generations](https://github.com/jiangjmj/Graph-based-Uncertainty) (Jiang et al., 2024).

## Setup

Tested with Python 3.11.

```bash
pip install -r requirements.txt
export OPENAI_API_KEY=<your key>   # or put it in a .env file
```

QASPER is downloaded automatically from the Hugging Face Hub.

## Knowledge expansion (QASPER)

Builds the weighted bipartite graph from the priors, routes Boundary claims to the GPT-4.1 verifier, and promotes verified claims to priors over three rounds.

```bash
python run_qasper_experiment.py --split test --num_samples 100 \
    --generator_model gpt-4o-mini --claim_extractor llm \
    --verifier_type llm --openai_model gpt-4.1 \
    --experiment_name expansion
```

## Question answering

Answers questions using the Grounded claims, graph-guided retrieval, and the abstract-only and full-paper baselines, then judges the answers with GPT-4.1.

```bash
python run_verified_claims_qa.py --full_pipeline \
    --results_path experiments/qasper/expansion/results.json \
    --experiment_name qa
```

Results are written to `experiments/qasper/`.
