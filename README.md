# RAG-Context-Faithfulness-Evaluation
Comparative evaluation of lexical, dense bi-encoder, and NLI cross-encoder models for detecting subtle RAG hallucinations.
Evaluating Lexical, Dense, and NLI Scoring for RAG Hallucination Detection

This repository contains a comparative study evaluating how well different NLP similarity and inference models detect subtle factual hallucinations in context-grounded question answering.

Standard embedding models often assign high cosine similarity to sentences that share vocabulary even when numbers, entities, or causal directions are inverted. In this experiment, I constructed a paired benchmark of valid paraphrases and subtle factual contradictions to measure how well three scoring methods separate faithful claims from hallucinations.

Methods Compared

1. TF-IDF Lexical Overlap
- Computes bag-of-words cosine similarity between the reference context and generated claim as a surface-level baseline.

2. Dense Bi-Encoder Similarity (all-MiniLM-L6-v2)
- Encodes the context and claim independently into normalized dense vectors and measures dot-product similarity.

3. Cross-Encoder NLI Entailment (nli-deberta-v3-small)
- Jointly encodes context-claim pairs using cross-attention and extracts the softmax entailment probability.

Key Findings

- Surface and Bi-Encoder Blindness: Both TF-IDF and dense bi-encoders struggled to penalize entity swaps and numerical errors, producing overlapping score distributions between faithful and hallucinated claims.
- Cross-Attention Separation: The NLI cross-encoder achieved strong ROC-AUC and PR-AUC separation by directly modeling logical entailment versus contradiction across tokens.

Files

- RAG_Faithfulness_Detector_Study.ipynb - Colab notebook with the evaluation dataset, scoring pipelines, ROC/PR metrics, and visualization code.
- rag_faithfulness_results.png - Comparison plots showing ROC curves and mean score separation across all three methods.
