---
title: "Offline Evaluation for Reinforcement Learning-based Recommendation - A Critical Issue and Some Alternatives"
date: 2023-02-03
coauthors: 
  - Romain Deffayet
  - Thibaut Thonet
  - Jean-Michel Renders
  - Maarten de Rijke
venue: SIGIR Forum
status: Published in
paper_url: https://sigir.org/wp-content/uploads/2023/01/p03.pdf
code_url: nourl
summary: "We discussed offline evaluation for RL-based recommender systems and noted that the most common evaluation protocol, i.e., next-item prediction, is unsuited to such approaches."
metaDescription: Published in SIGIR Forum.
tags:
  - Reinforcement Learning
  - Recommendation
  - Offline Evaluation
  - Selected_publication
---
We discussed offline evaluation for RL-based recommender systems and noted that the most common evaluation protocol, i.e., next-item prediction, is unsuited to such approaches.

Definition of next-item prediction:
Next-item prediction (NIP) is an offline evaluation protocol for sequential itemrecommendation from real user feedback. The task is to ensure that the next interacted itemis among the top items ranked by the model, given the sequence of past interactions. Modelperformance is measured according to ranking metrics (e.g., hit rate, recall, NDCG, etc).

Among the 24 papers performing offline eval of RL-based RecSys, 22 used this protocol. But we argue that (1) it is myopic and does not account for long-term outcomes, (2) what it considers as ground truth is suboptimal and (3) it hides deficiencies of RL agents trained offline.

(1) RL agents optimize whole sequences to improve long-term outcomes. But by incentivizing greedy optimization of the next action, NIP may encourage accurate but myopic agents, at the cost of diversity or novelty. This is known to lead to boredom and lower long-term satisfaction.

(2) Another argument for RL is its open-ended objective : it may recover novel policies by maximizing rewards. But NIP evaluates whether agents predict the next observed item. This is likely a suboptimal target, and prevents recommendations that would have led to higher rewards.

(3) RL agents trained offline are known to overestimate the Q-value on unseen actions, and thus underperform during deployment ( https://arxiv.org/abs/1812.02648).
This is due to the optimizer's curse, i.e., the agent selects the action with highest Q-value, which is likely overestimated. But NIP hides this issue. While A/B tests evaluate how good the selected action is, NIP evaluates how high the target item is ranked in the agent's internal preferences. E.g., a model placing the target item as second-best may have Recall@2=1 yet be arbitrarily bad when deployed.

In conclusion, the next-item prediction protocol counters the very motivations for RL-based recommenders (going beyond accuracy, maximizing long-term outcomes, recovering novel policies), while also hiding their deficiencies when trained in an off-policy manner.

We therefore encourage researchers to use other methods to evaluate RL recommenders. While all of these methods have drawbacks that we detail in the paper, we notably recommend counterfactual OPE such as IPS, semi-synthetic simulators and uncertainty-aware evaluation.