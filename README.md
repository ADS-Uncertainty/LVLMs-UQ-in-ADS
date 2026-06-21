# Quantifying Prediction Uncertainty of Large Vision-Language Models for Autonomous Driving: An Empirical Study

<p align="center">
  <img src="https://raw.githubusercontent.com/ADS-Uncertainty/LVLMs-UQ-in-ADS/124c4490f3bf27045e330a939390968d9adf3552/Image/overview-Github.png" width="1200">
</p>

## Abstract
Large Vision-Language Models (LVLMs) have demonstrated strong potential in Autonomous Driving Systems (ADS). However, their inherent uncertainty raises concerns regarding safety during real-world deployment. Studies on LVLM uncertainty quantification mostly focus on simple vision-language tasks by assuming ideal and unperturbed visual conditions. Systematically quantifying uncertainty of LVLMs in performing ADS tasks largely remain unexplored. In this article, we present a very first empirical study that quantifies the prediction uncertainty of 10 open-source LVLMs across 8 ADS tasks, and evaluates their performance under 7 types of image corruptions. Results show that in ADS tasks, prediction uncertainty and prediction performance of LVLMs do not always align, and relying on a single metric for evaluation may overlook critical safety risks; snow and zoom blur have the greatest effect, leading to an average increase in prediction uncertainty of 11.1\% and 9.3\% per LVLM, respectively; image corruptions do not increase LVLMs’ prediction uncertainty across all ADS tasks, e.g., in traffic light perception, 90\% of LVLMs’ uncertainty paradoxically decreased; and within the same model family, LVLMs with larger parameter scales tend to exhibit lower prediction uncertainty and thus handle corruptions more robustly. We introduce the NuplanQA-UQ dataset to support further assessment of LVLM uncertainty in the context of ADS.


## Overview
This repository contains the code, experimental results, and scripts required to reproduce the findings of our article, *Quantifying Prediction Uncertainty of Large Vision-Language Models for Autonomous Driving: An Empirical Study*. Additionally, we provide two sets of preliminary experimental results:
- Effect of input format (six-view concatenation vs. per-image inputs) on LVLM performance.
- Effect of sampling size (5 vs. 10 samples) on LVLM performance and uncertainty.

The artifact includes:
1. Dataset: NuplanQA-UQ
2. Scripts to download the NuPlan and NuPlanQA-Eval datasets.
3. Code to perform predictions using the 10 open-source LVLMs employed in the study, and to obtain the raw experimental outputs.
4. Scripts to compute evaluation metrics reported in the paper based on the raw experimental results.
5. The final experimental results, which can be used to directly reproduce the uncertainty quantification results and other findings presented in the study.


## 📦 NuplanQA-UQ dataset Collection
The NuplanQA-UQ dataset (1.8G) can be downloaded from:
https://pan.baidu.com/s/1Oj9lRicESIz5xqys8e_rag

Access code: 97yf

## Preliminary Experiment-I: Effect of Input Format (Six-View Concatenation vs. Per-Image Inputs) on LVLM Performance
- To investigate whether image input formats affect the prediction performance of different LVLMs, we conduct preliminary experiments on LVLMs with fewer than 10B parameters. Specifically, NuPlanQA-Eval consists of 8 ADS tasks, i.e., (1) traffic light perception, (2) road characteristics perception, (3) surrounding objects recognition, (4) key object recognition, (5) traffic flow recognition, (6) ego-centric situation assessment, (7) ego-centric action recommendation, and (8) ego vehicle (EV) maneuver reasoning, each containing approximately 200 samples. We randomly sample 5 instances from each task to construct a validation subset, resulting in a total of 40 samples (8 tasks × 5 samples). On this subset, we evaluate different image input formats, including six-view concatenation and per-image multiple-input settings, and report the prediction accuracy of LVLMs. All experiments are conducted under the clean condition with a sampling size of five. The experimental results are shown in the figure below.

<p align="center">
  <img src="https://raw.githubusercontent.com/ADS-Uncertainty/LVLMs-UQ-in-ADS/dbb15f1c95f23afa2e90856f205f8b54dfb81dd0/Image/6vs1.png" width="700">
</p>

- It can be observed that the prediction accuracy of LVLMs does not exhibit significant variation across different image input formats, and the overall trends remain largely consistent. Given the limited size of the subset (40 samples), we conclude that the impact of input format on both LVLM prediction accuracy and uncertainty is negligible. Therefore, the performance differences among LVLMs are primarily attributed to their intrinsic model capabilities or the scope of their pretraining data, rather than the input format.



## Preliminary Experiment-II: Effect of Sampling Size (5 vs. 10 samples) on LVLM Performance and Uncertainty
- To evaluate how the number of sampling runs affects the experimental results of LVLMs, we conduct preliminary experiments on a validation subset of 40 samples from NuPlanQA-Eval (see Preliminary Experiment I). Specifically, we perform 5 sampling runs (ours) and 10 sampling runs for each LVLM, and report the corresponding results below.

<p align="center">
  <img src="https://raw.githubusercontent.com/ADS-Uncertainty/LVLMs-UQ-in-ADS/5b12ca204ebd16ef63325a7594288d6910b79729/Image/5%20vs%2010%20Samples.png" width="800">
</p>

- From Table X, it can be observed that under 10 sampling runs, the average prediction accuracy of LVLMs remains almost identical to that under 5 sampling runs. The prediction uncertainty shows a slight increase when increasing the number of sampling runs from 5 to 10. Considering that the uncertainty values lie within the range [0, 1.922), the average increase of 7.2% is reasonable, as a larger number of samples is more likely to introduce additional response diversity, especially under image perturbations.
- Overall, the ranking of LVLMs in terms of both prediction performance and uncertainty remains highly consistent with that reported in our main paper. For instance, InternVL-3-8B still achieves the best performance with the lowest uncertainty, while Deepseek-VL2-3B remains the worst-performing model. This further validates the reliability of our experimental findings.
- We recommend using a larger number of sampling runs for uncertainty quantification of LVLMs when computational resources permit, as it generally leads to more reliable uncertainty estimation.

