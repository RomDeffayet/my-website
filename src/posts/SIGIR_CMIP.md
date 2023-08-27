---
title: An Offline Metric for the Debiasedness of Click Models
date: 2023-04-11
venue: SIGIR'23
status: Accepted at
paper_url: https://arxiv.org/abs/2304.09560
code_url: https://github.com/philipphager/cmip
coauthors: 
  - Romain Deffayet
  - Philipp Hager
  - Jean-Michel Renders
  - Maarten de Rijke
summary: Click models aim to identify and extract biases in search data, but we do not evaluate whether they actually do so. We propose a metric based on relevance annotations that measures the debiasedness of click models, and consequently their usefulness in learning-to-rank from implicit feedback.
metaDescription: Accepted at SIGIR23
tags:
  - Click Models
  - ULTR
  - Offline Evaluation
  - Selected_publication
---

One can't judge a click model only by how well it ranks documents, we also need to make sure it actively identified and removed biases hidden in the logged data.

Remember when we [analyzed lots of click models and found many of them are not able to predict accurate click probabilities on unseen rankings](https://www.deffayet.cc/posts/evaluating-the-robustness-of-click-models-to-policy-distributional-shift/) ? 
Well, we found a way to detect this failure without actually deploying these models to the downstream task.

Picture students taking an exam, where they have the possibility to cheat by copying on a good classmate. How do you differentiate those whose truly understood the course from those who cheated ?

Comparing their grade doesn't work, because they could match the classmate just by copying. They can even reach a better grade by combining cheating and their own knowledge ! 
You must compare the mistakes to spot the cheaters: those making the same ones as the classmate cheated.

That's the idea of our metric: analyze the correlations between relevance scores predicted by the logging policy (the reference classmate) and by the candidate click model.  If they are correlated beyond the true relevance signal, the model failed to debias the logged data.
![CMIP](/src/assets/img/CMIP.png)

We defined the "debiasedness" of a click model as the independence of its predicted scores and those of the LP, conditionally to relevance labels. In other words, a model is debiased if one cannot guess its prediction by revealing where the LP placed the considered document.

By computing the conditional mutual information of these quantities, our metric CMIP measures how debiased a model is.  
While debiasedness alone is not sufficient (a random click model is debiased), CMIP helps to discard biased models and predict out-of-distribution metrics.
![CMIP](/src/assets/img/CMIP_example.png)

In the paper, we explain CMIP in more details and systematically assess its reliability for click model evaluation.  
CMIP, like nDCG, requires relevance annotations which can be obtained, e.g., via human labeling or using randomized traffic (we leave the latter for future work).

Our code is open-source (https://github.com/philipphager/sigir-cmip) and we release a standalone implementation of CMIP to help learning-to-rank practitioners use it in their scenarios (https://github.com/philipphager/cmip)
