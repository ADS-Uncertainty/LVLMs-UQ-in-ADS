# Quantifying Prediction Uncertainty of Large Vision-Language Models for Autonomous Driving: An Empirical Study

<p align="center">
  <img src="https://raw.githubusercontent.com/ADS-Uncertainty/LVLMs-UQ-in-ADS/124c4490f3bf27045e330a939390968d9adf3552/Image/overview-Github.png" width="1200">
</p>

## Abstract
Large Vision-Language Models (LVLMs) have demonstrated strong potential in Autonomous Driving Systems (ADS). However, their inherent uncertainty raises concerns regarding safety during real-world deployment. Studies on LVLM uncertainty quantification mostly focus on simple vision-language tasks by assuming ideal and unperturbed visual conditions. Systematically quantifying uncertainty of LVLMs in performing ADS tasks largely remain unexplored. In this article, we present a very first empirical study that quantifies the prediction uncertainty of 10 open-source LVLMs across 8 ADS tasks, and evaluates their performance under 7 types of image corruptions. Results show that in ADS tasks, prediction uncertainty and prediction performance of LVLMs do not always align, and relying on a single metric for evaluation may overlook critical safety risks; snow and zoom blur have the greatest effect, leading to an average increase in prediction uncertainty of 11.1\% and 9.3\% per LVLM, respectively; image corruptions do not increase LVLMs’ prediction uncertainty across all ADS tasks, e.g., in traffic light perception, 90\% of LVLMs’ uncertainty paradoxically decreased; and within the same model family, LVLMs with larger parameter scales tend to exhibit lower prediction uncertainty and thus handle corruptions more robustly. We introduce the NuplanQA-UQ dataset to support further assessment of LVLM uncertainty in the context of ADS.


## Overview
- This repository contains the code, experimental results, and scripts required to reproduce the findings of our article, *Quantifying Prediction Uncertainty of Large Vision-Language Models for Autonomous Driving: An Empirical Study*.
- Additionally, we provide preliminary results on the impact of input format (six-view image concatenation versus individual image inputs) on LVLM performance.

- The artifact includes:
1. Dataset: NuplanQA-UQ
2. Scripts to download the NuPlan and NuPlanQA-Eval datasets.
3. Code to perform predictions using the 10 open-source LVLMs employed in the study, and to obtain the raw experimental outputs.
4. Scripts to compute evaluation metrics reported in the paper based on the raw experimental results.
5. The final experimental results, which can be used to directly reproduce the uncertainty quantification results and other findings presented in the study.


## 📦 NuplanQA-UQ dataset Collection
The NuplanQA-UQ dataset (1.8G) can be downloaded from:
https://pan.baidu.com/s/1Oj9lRicESIz5xqys8e_rag

Access code: 97yf

## 🧾 Preliminary Experiment-I: Effect of Input Format (Six-View Concatenation vs. Per-Image Inputs) on LVLM Performance
- To investigate whether image input formats affect the prediction performance of different LVLMs, we conduct preliminary experiments on LVLMs with fewer than 10B parameters. Specifically, NuPlanQA-Eval consists of 8 ADS tasks, i.e., (1) traffic light perception, (2) road characteristics perception, (3) surrounding objects recognition, (4) key object recognition, (5) traffic flow recognition, (6) ego-centric situation assessment, (7) ego-centric action recommendation, and (8) ego vehicle (EV) maneuver reasoning, each containing approximately 200 samples. We randomly sample 5 instances from each task to construct a validation subset, resulting in a total of 40 samples (8 tasks × 5 samples). On this subset, we evaluate different image input formats, including six-view concatenation and per-image multiple-input settings, and report the prediction accuracy of LVLMs. All experiments are conducted under the clean condition with a sampling size of five. The experimental results are shown in the figure below.

<p align="center">
  <img src="https://raw.githubusercontent.com/ADS-Uncertainty/LVLMs-UQ-in-ADS/dbb15f1c95f23afa2e90856f205f8b54dfb81dd0/Image/6vs1.png" width="700">
</p>

- It can be observed that the prediction accuracy of LVLMs does not exhibit significant variation across different image input formats, and the overall trends remain largely consistent. Given the limited size of the subset (40 samples), we conclude that the impact of input format on both LVLM prediction accuracy and uncertainty is negligible. Therefore, the performance differences among LVLMs are primarily attributed to their intrinsic model capabilities or the scope of their pretraining data, rather than the input format.

