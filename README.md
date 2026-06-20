# Quantifying Prediction Uncertainty of Large Vision-Language Models for Autonomous Driving: An Empirical Study

<p align="center">
  <img src="https://raw.githubusercontent.com/ADS-Uncertainty/LVLMs-UQ-in-ADS/124c4490f3bf27045e330a939390968d9adf3552/Image/overview-Github.png" width="900">
</p>
https://github.com/ADS-Uncertainty/LVLMs-UQ-in-ADS/blob/124c4490f3bf27045e330a939390968d9adf3552/Image/overview-Github.png



## Abstract
Large Vision-Language Models (LVLMs) have demonstrated strong potential in Autonomous Driving Systems (ADS). However, their inherent uncertainty raises concerns regarding safety during real-world deployment. Studies on LVLM uncertainty quantification mostly focus on simple vision-language tasks by assuming ideal and unperturbed visual conditions. Systematically quantifying uncertainty of LVLMs in performing ADS tasks largely remain unexplored. In this article, we present a very first empirical study that quantifies the prediction uncertainty of 10 open-source LVLMs across 8 ADS tasks, and evaluates their performance under 7 types of image corruptions. Results show that in ADS tasks, prediction uncertainty and prediction performance of LVLMs do not always align, and relying on a single metric for evaluation may overlook critical safety risks; snow and zoom blur have the greatest effect, leading to an average increase in prediction uncertainty of 11.1\% and 9.3\% per LVLM, respectively; image corruptions do not increase LVLMs’ prediction uncertainty across all ADS tasks, e.g., in traffic light perception, 90\% of LVLMs’ uncertainty paradoxically decreased; and within the same model family, LVLMs with larger parameter scales tend to exhibit lower prediction uncertainty and thus handle corruptions more robustly. We introduce the NuplanQA-UQ dataset to support further assessment of LVLM uncertainty in the context of ADS.

## Overview
This repository contains the code, experimental results, and scripts required to reproduce the findings of our article:
The artifact includes:
1. Dataset: NuplanQA-UQ
2. Scripts to download the NuPlan and NuPlanQA-Eval datasets.
3. Code to perform predictions using the 10 open-source LVLMs employed in the study, and to obtain the raw experimental outputs.
4. Scripts to compute evaluation metrics reported in the paper based on the raw experimental results.
5. The final experimental results, which can be used to directly reproduce the uncertainty quantification results and other findings presented in the study.


## Preliminary Experiment-I: Effect of Input Format (Six-View Concatenation vs. Per-Image Inputs) on LVLM Performance
<p align="center">
  <img src="https://raw.githubusercontent.com/ADS-Uncertainty/LVLMs-UQ-in-ADS/dbb15f1c95f23afa2e90856f205f8b54dfb81dd0/Image/6vs1.png" width="700">
</p>

## Preliminary Experiment-II: Effect of Sampling Size (5 vs. 10) on LVLM Performance and Uncertainty

<p align="center">
  <img src="https://raw.githubusercontent.com/ADS-Uncertainty/LVLMs-UQ-in-ADS/f2c9c99a19b850fb6a8559539de985a0aca03ddb/Image/sampling.png" width="800">
</p>
