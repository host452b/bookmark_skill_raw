Every model in our catalog generates responses to the same set of standardized prompts. From each text response, we extract a **32-dimension stylometric fingerprint** covering lexical richness, sentence structure, punctuation habits, formatting preferences, and discourse patterns (hedging, boosting, transitions, etc.).

Per-model fingerprints are the mean of all individual response fingerprints (minimum 3 text responses required). Before computing similarity, all features are **z-score normalized** to prevent high-magnitude features (like sentence_length_variance) from dominating the comparison.

Pairwise similarity uses **cosine similarity** on the normalized 32-dimension vectors. Clone detection uses a threshold of 0.90 (top 0.08% of all pairs). Price arbitrage compares models with &gt; 0.75 similarity using a weighted average price (3:1 output:input ratio).

Provider distinctiveness is the ratio of average intra-provider similarity to inter-provider similarity. Values &gt; 1 indicate a detectable house writing style.

**Raw response analysis** goes deeper: for each of the 43 standardized prompts, we compute per-challenge pairwise similarity across all responding models. This produces prompt-controlled head-to-head scores (same prompt, same conditions). A "confidence" metric (avg similarity / (1 + stddev)) identifies pairs that are consistently similar across many prompts, not just similar on average. Prompt-dependent twins are pairs with high average but high variance, meaning the prompt determines whether they converge.

Total corpus: 3,095 responses across 178 models and 43 standardized prompts. Analysis recomputed with each model addition.