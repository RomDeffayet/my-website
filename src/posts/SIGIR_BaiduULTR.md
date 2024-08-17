---
title: "Unbiased Learning to Rank Meets Reality: Lessons from Baidus Large-Scale Search Dataset"
date: 2024-07-14
venue: SIGIR'24
status: Accepted at
paper_url: https://dl.acm.org/doi/abs/10.1145/3626772.3657892
code_url: https://github.com/philipphager/ultr-reproducibility
coauthors: 
  - Philipp Hager
  - Romain Deffayet
  - Jean-Michel Renders
  - Onno Zoeter
  - Maarten de Rijke
summary: We tried to reproduce famous unbiased learning-to-rank results on the large Baidu-ULTR dataset. It turned out that it does not work as intended ... or at least that success depends on how your measure success.
metaDescription: Accepted at SIGIR24
tags:
  - Click Models
  - ULTR
  - Selected_publication
---


![ULTR_results](/src/assets/img/baidu_ULTR_main.jpeg)

ULTR aims to estimate the relevance of search results by learning from the click logs that search engines can collect. Without correction, ML models will replicate biases from their training data: for instance, top-ranked documents are clicked much more often than bottom ones.

So far, ULTR had mostly been tested in simulations. Last year, Baidu's search team released a massive dataset of search sessions with clicks and human annotations of relevance. That was a tremendous opportunity to benchmark ULTR techniques in a large-scale, real-world setting.

We extensively and carefully compared prominent unbiased learning-to-rank methods on this dataset, across multiple representations and training schemes. For every bias correction method, we also trained its non-correcting equivalent.

We found that:
✅ Bias modeling techniques find a substantial bias and agree with each other on its scale
✅ Bias correction robustly improves the accuracy of click prediction
❌ Bias correction does not improve how well models agree with human annotators

This puzzling finding suggests that annotators and actual users may disagree on how good a search result is. There is no single universal choice for improving search engines: re-ranking results to maximize click rates and predicting generic relevance scores are different tasks.

We should strive to understand the connections and differences between annotations and clicks, and when to prioritize one metric over the other. For now, we discuss additional observations and potential explanations for these results in our paper.
This work was first and foremost an effort to make ULTR more accessible, so we release:
- Jax-based implementations for all methods, including BERT-like training for document features: https://github.com/philipphager/ultr-reproducibility
- Models and pre-processed datasets: https://huggingface.co/philipphager
