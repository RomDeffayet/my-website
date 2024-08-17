---
title: "SARDINE: A Simulator for Automated Recommendation in Dynamic and Interactive Environments"
date: 2024-08-01
coauthors: 
  - Romain Deffayet
  - Thibaut Thonet
  - Dongyoon Hwang
  - Vassilissa Lehoux
  - Jean-Michel Renders
  - Maarten de Rijke
venue: ACM TORS
status: Published in
paper_url: https://dl.acm.org/doi/full/10.1145/3656481
code_url: https://github.com/naver/sardine
summary: "We built a simulator that accounts for the dynamic and interactive nature of recommender systems. Off-the-shelf RL baselines are not able to solve the tasks we propose."
metaDescription: Published in ACM TORS.
tags:
  - Simulator
  - Recommendation
  - Slate Recommendation
  - Reinforcement Learning
  - ULTR
---

Simulators can provide valuable insights for researchers and practitioners who wish to improve recommender systems, because they allow one to easily tweak the experimental setup in which recommender systems operate, and as a result lower the cost of identifying general trends and uncovering novel findings about the candidate methods. A key requirement to enable this accelerated improvement cycle is that the simulator is able to span the various sources of complexity that can be found in the real recommendation environment that it simulates.
With the emergence of interactive and data-driven methods—e.g., reinforcement learning or online and counterfactual learning-to-rank—that aim to achieve user-related goals beyond the traditional accuracy-centric objectives, adequate simulators are needed. In particular, such simulators must model the various mechanisms that render the recommendation environment dynamic and interactive, e.g., the effect of recommendations on the user or the effect of biased data on subsequent iterations of the recommender system. We therefore propose SARDINE, a flexible and interpretable recommendation simulator that can help accelerate research in interactive and data-driven recommender systems. We demonstrate its usefulness by studying existing methods within nine diverse environments derived from SARDINE, and even uncover novel insights about them.
