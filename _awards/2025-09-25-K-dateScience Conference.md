---
layout: award
title: "2025 K-DataScienc Conference"
subtitle: "2025 K-DataScienc Conference Project"
start_date: 2025-05-20
end_date: 2025-09-05
featured_image: "images/awards/"
published: true
---


## 🏆 Future Research Award
### 2025 K-Data Science Conference (Research & Poster Presentation)

<br/>

## 📌 Problem Statement
<div style="text-align: center; margin: 24px 0;">
  <img src="/images/awards/2025-09-25-K-dateScience Conference/kds_problem_1.png" alt="Mathematical reasoning problem illustration" style="max-width: 1000px; width: 100%; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.09);">
  <p style="font-size: 0.92em; color: #666; margin-top: 8px;">High Math-500 accuracy is primarily achieved by large-scale LLMs, while compact models remain underrepresented, with LFM showing limited performance.</p>
</div>
Recent advances in large language models (LLMs) have demonstrated strong performance in general language understanding; however, **mathematical reasoning remains a challenging domain**, particularly under resource-constrained settings.  
Most existing approaches rely on large-scale models or supervised fine-tuning (SFT), which limits practical deployment and increases data dependency.

This project addresses the following research question:  
**Can mathematical reasoning ability be significantly improved using reinforcement learning alone, without supervised fine-tuning, on a compact language model?**

<br/>
## 💡 Proposed Solution

### (1) Curriculum Learning
<div style="text-align:center; margin:20px 0 36px 0;">
  <img src="/images/awards/2025-09-25-K-dateScience Conference/kds_method_1.png"
       alt="Curriculum Learning Strategy"
       style="width:100%; max-width:760px; border-radius:10px; box-shadow:0 4px 10px rgba(0,0,0,0.1);">
  <p style="font-size:0.95em; color:#555; margin-top:10px;">
    The training process progresses from easy to hard problems, enabling stable reasoning acquisition and preventing early-stage failure.
  </p>
</div>

### (2) KL-free Policy Optimization (ZeroGRPO)
<div style="text-align:center; margin:20px 0 36px 0;">
  <img src="/images/awards/2025-09-25-K-dateScience Conference/kds_method_2.png"
       alt="KL-free Policy Optimization"
       style="width:100%; max-width:760px; border-radius:10px; box-shadow:0 4px 10px rgba(0,0,0,0.1);">
  <p style="font-size:0.95em; color:#555; margin-top:10px;">
    Removing the KL-divergence constraint allows compact models to freely explore diverse reasoning trajectories.
  </p>
</div>

### (3) Simple Reward Design with Reasoning-Length Penalty
<div style="text-align:center; margin:20px 0 36px 0;">
  <img src="/images/awards/2025-09-25-K-dateScience Conference/kds_method_3.png"
       alt="Reward Design with Length Penalty"
       style="width:100%; max-width:760px; border-radius:10px; box-shadow:0 4px 10px rgba(0,0,0,0.1);">
  <p style="font-size:0.95em; color:#555; margin-top:10px;">
    A minimal reward based on answer correctness and format validity, combined with a mild penalty on excessively long reasoning.
  </p>
</div>

Together, these three components form a unified reinforcement-learning framework that enables effective mathematical reasoning in compact language models without increasing model size or supervision cost.



<br/>

## 🛠️ Technical Overview
- **Base Model**:  
  - DeepSeek-R1-Distill-Qwen-1.5B (text-only lightweight LLM)
- **Training Method**:  
  - Reinforcement learning using a modified GRPO framework
  - Removal of KL-divergence regularization to allow unconstrained policy exploration
- **Key Techniques**:  
  - Zero-KL policy optimization (ZeroGRPO)
  - Simple and stable reward design based on answer correctness and format consistency
  - Curriculum learning strategy with progressively increasing difficulty
- **Evaluation Benchmark**:  
  - Math-500 benchmark covering multiple mathematical domains and difficulty levels

<br/>

## 🎬 Results and Achievements
<div style="
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 18px;
  margin-bottom: 30px;
">

  <div style="
    height: 220px;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    border-radius: 8px;
    background: #fff;
    box-shadow: 0 3px 6px rgba(0,0,0,0.08);
  ">
    <img src="../images/awards/2025-09-25-K-dateScience Conference/kds_result_1.png"
         style="width:100%; height:100%; object-fit: contain;">
  </div>

  <div style="
    height: 220px;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    border-radius: 8px;
    background: #fff;
    box-shadow: 0 3px 6px rgba(0,0,0,0.08);
  ">
    <img src="../images/awards/2025-09-25-K-dateScience Conference/kds_result_2.png"
         style="width:100%; height:100%; object-fit: contain;">
  </div>

  <div style="
    height: 220px;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    border-radius: 8px;
    background: #fff;
    box-shadow: 0 3px 6px rgba(0,0,0,0.08);
  ">
    <img src="../images/awards/2025-09-25-K-dateScience Conference/kds_result_3.png"
         style="width:100%; height:100%; object-fit: contain;">
  </div>

</div>


- **Substantial Performance Improvement**:
  - Achieved up to **3.7× accuracy improvement** over the base model on Math-500
  - Outperformed standard GRPO and penalty-based variants under identical settings
- **Efficiency and Practicality**:
  - Demonstrated that strong mathematical reasoning can be achieved with a **1.5B-parameter model**
  - No supervised fine-tuning required, reducing data and annotation costs
- **Research Contribution**:
  - Validated that removing KL constraints is particularly beneficial for small models
  - Showed the effectiveness of curriculum learning in stabilizing RL-based reasoning training
- **Outcome**:
  - Research results accepted for **poster presentation** at the 2025 K-Data Science Conference
  - Selected as a **funded research project** by the conference committee

<br/>

## Commemorative Photo
<div style="
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 14px;
  margin: 24px 0;
">

  <img src="../images/awards/2025-09-25-K-dateScience Conference/kds_commemorate_1.jpg"
       style="width:100%; border-radius:10px;">

  <img src="../images/awards/2025-09-25-K-dateScience Conference/kds_commemorate_2.jpg"
       style="width:100%; border-radius:10px;">

  <img src="../images/awards/2025-09-25-K-dateScience Conference/kds_commemorate_3.jpg"
       style="width:100%; border-radius:10px;">

</div>

