---
title: Evaluating the Robustness of Click Models to Policy Distributional Shift
date: 2020-10-15T12:23:39.598Z
coauthors: 
  - Romain Deffayet
  - Jean-Michel Renders
  - Maarten de Rijke
venue: ACM TOIS
status: Published in
paper_url: https://dl.acm.org/doi/abs/10.1145/3569086
code_url: https://github.com/naver/dist-shift-click-models
summary: "We investigated how click models *actually* perform (spoiler: not so
  great), and whether our offline metrics capture this (spoiler 2: they don't).
  Here's what it means for ULTR researchers and practitioners."
metaDescription: Published in ACM TOIS.
tags:
  - Click Models
  - ULTR
---
We investigated how click models *actually* perform (spoiler: not so great), and whether our offline metrics capture this (spoiler 2: they don't). Here's what it means for ULTR researchers and practitioners.

First, some context: training click models is a way to obtain the propensities used in UL2R by learning directly from logged data. While their training objective is to learn to predict clicks, their true goal is to recover accurate relevance and propensity estimates.

The standard evaluation is simple: we use log-likelihood or perplexity to evaluate the goodness-of-fit of our model, and nDCG with respect to relevance annotations to evaluate its debiasing capabilities: the higher the nDCG, the more accurate the relevance/propensity prediction.

But something's troubling: very naive and obviously biased baselines (for example counting the number of impressions of each item) obtain much higher nDCG than all recent click models !

We explain in the paper that it happens because the logging policy is usually a strong predictor of relevance, and replicating its biases secures a high nDCG: this protocol doesn't evaluate whether we debiased the data. It therefore casts a doubt on recent improvements of CMs.

We simulate "deployments" (i.e. OPEs) in a semi-synthetic setup where only the true user click model is simulated. It turns out that simpler models (PBM, UBM) are better than more complex models at OPE across a wide range of user models and policy distributional shifts.

We also acknowledge that nowadays, click models are used for more than just OPE : offline bandit/RL training, fairness, etc. These tasks are more demanding because they are subject to the optimizer's curse. Our simulations show that complex CMs return highly suboptimal policies.

The lack of robustness in off-policy settings, and more importantly the fact that offline metrics cannot capture it, is critical to the field of UL2R which often assumes perfect propensities, and probably even more to demanding tasks such as RL and fairness of exposure.

Our semi-synthetic protocol can be adapted to any search engine and helps mitigating the risks of poor robustness, but more work is needed to correctly evaluate debiasing models.
