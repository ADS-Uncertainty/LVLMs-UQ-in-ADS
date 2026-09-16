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
The NuplanQA-UQ dataset (1.8G) can be downloaded from: https://doi.org/10.5281/zenodo.22643782

## 🧾 Experimental Setup: Prompt Design and Result Collection
- For the evaluation of all LVLMs, we followed the experimental protocol of **NuplanQA-Eval** and used the same system prompt for all models during inference to ensure a consistent evaluation setting. The complete system prompt is provided below:


    - [System Prompt] You are driving from inside the vehicle cabin. The image shows six views from the ego vehicle, arranged in two rows from left to right: front left, front, and front right on the top row; back right, back, and back left on the bottom row.
The prompt provides additional information extracted from your vehicle, sampled 5 times over the past 1.5 seconds. Use the changes in velocity and steering angle to determine whether the vehicle is slowing down, accelerating, turning, curving, changing lanes, or making adjustments. Note that negative steering angles indicate a right turn, while positive angles indicate a left turn.

- Notably, **we appended the instruction “Provide the selected answer choice only.” to each user prompt**, for example, “What is the most appropriate maneuver given the current conditions? Provide the selected answer choice only.” This instruction was used to standardize the response format across different LVLMs and facilitate reliable extraction and evaluation of their predicted answers. Finally, **we programmatically validated the response format for all outputs and manually inspected ambiguous or invalid responses to ensure the correct collection and computation of the experimental results**.


## 🧾 Preliminary Experiment-I: Effect of Input Format (Six-View Concatenation vs. Per-Image Inputs) on LVLM Performance
- To investigate whether image input formats affect the prediction performance of different LVLMs, we conducted preliminary experiments on LVLMs with fewer than 10B parameters. Specifically, NuPlanQA-Eval consists of 8 ADS tasks, i.e., (1) traffic light perception, (2) road characteristics perception, (3) surrounding object recognition, (4) key object recognition, (5) traffic flow recognition, (6) ego-centric situation assessment, (7) ego-centric action recommendation, and (8) ego vehicle (EV) maneuver reasoning, each containing approximately 200 samples. We randomly sampled 5 instances from each task to construct a validation subset, resulting in a total of 40 samples (8 tasks × 5 samples). On this subset, we evaluated different image input formats, including six-view concatenation and per-image multiple-input settings, and reported the prediction accuracy of LVLMs. All experiments were conducted under the clean condition with five sampling runs. The experimental results are shown in the figure below.

<p align="center">
  <img src="https://raw.githubusercontent.com/ADS-Uncertainty/LVLMs-UQ-in-ADS/dbb15f1c95f23afa2e90856f205f8b54dfb81dd0/Image/6vs1.png" width="700">
</p>

- As shown in the figure, although some model-specific differences in prediction accuracy were observed, the overall performance trends and relative rankings of the LVLMs remained broadly consistent across the two input formats. Given the limited subset of 40 samples, these results provide preliminary evidence that input format is unlikely to be the primary factor driving cross-model performance differences.


## 🧾 Preliminary Experiment-II: Effect of the Number of Sampling Runs (Five vs. Ten Runs) on LVLM Performance and Uncertainty
- **Because repeated stochastic inference with LVLMs is computationally expensive**, particularly for models with **more than 7 billion parameters**, a large number of runs per input (e.g., more than ten) is impractical on large-scale test sets. In our study, **following [1]**, we generated five independent predictions for each input to compute Shannon entropy for uncertainty quantification, which is a setting commonly adopted in the evaluation of LLMs and LVLMs and provides a practical trade-off between computational feasibility and reliable characterization of output variability [2]. In total, 633,600 predictions were performed (10 LVLMs × 8 visual conditions × 1,584 inputs × 5 runs).
- To evaluate how the number of sampling runs affected the experimental results, we conducted a supplementary sensitivity experiment on a validation subset of 40 samples from NuPlanQA-Eval (see Preliminary Experiment I). Specifically, we compared the results obtained using five and ten independent sampling runs for eight representative LVLMs, as reported below.

<p align="center">
  <img src="https://raw.githubusercontent.com/ADS-Uncertainty/LVLMs-UQ-in-ADS/5b12ca204ebd16ef63325a7594288d6910b79729/Image/5%20vs%2010%20Samples.png" width="800">
</p>

- As shown in the table, under ten sampling runs, the average prediction accuracy of LVLMs remains almost identical to that under five sampling runs.
- The prediction uncertainty shows a slight increase when increasing the number of sampling runs from five to ten. This slight variation is reasonable, as a larger number of samples may introduce additional response diversity, especially under image corruptions. Moreover, **the ranking of LVLMs in terms of both prediction performance and uncertainty remains highly consistent with that reported in our main paper**. For instance, InternVL-3-8B still achieves the best performance with the lowest uncertainty, while DeepSeek-VL2-3B remains the worst-performing model. These preliminary results suggest that five sampling runs are sufficient to support the aggregate model comparisons and ranking-based conclusions reported in our study.

**References**

[1] R. Zhang, H. Zhang, and Z. Zheng, “Vl-uncertainty: Detecting hallucination in large vision-language model via uncertainty estimation,” 2024,
arXiv:2411.11919.

[2] A. Vazhentsev, E. Fadeeva, R. Xing, et al., “Unconditional Truthfulness: Learning Unconditional Uncertainty of Large Language Models,” in Proceedings of the 2025 Conference on Empirical Methods in Natural Language Processing (EMNLP), pp. 35673–35694, 2025.
