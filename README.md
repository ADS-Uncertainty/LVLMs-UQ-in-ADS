# Main Responses
---
- **Review A - Q1**: Clarify why expected RQ findings remain essential for
future ADS studies.
- **Response**: Although the high-level trend that corruption may degrade LVLM
performance is expected, its quantitative characterization remains
essential for ADS. **Our study identifies the severity,
corruption/task/model-scale dependence, and uncertainty--performance
relationship of LVLM behavior under corrupted inputs.** Notably, RQ2.2
shows that **90% of LVLMs exhibit reduced uncertainty but lower accuracy
in traffic-light perception**, indicating potentially overconfident
predictions that may threaten safety-critical ADS. Given the strong potential of LVLMs in future ADS applications [6],
our work provides the first systematic analysis of their uncertainty and
**offers empirical insights for robustness benchmarking,
uncertainty-aware monitoring, data augmentation, model optimization, and
safe deployment decisions**. In the next revision, we **will better
explain potential usages** of our findings in detail.



- **Review A - Q2**: Clarify what actionable guidelines can be drawn from
the experimental results.
- **Response**: Thank you for this valuable suggestion. We totally agree that the
experimental results should be translated into clearer practical
implications. In the revised manuscript, we **will add an "Actionable
Guidelines" paragraph in the Discussion section**. Specifically, we now
summarize five guidelines derived from our RQ1-RQ4 results: (1) evaluate
LVLMs using both accuracy and uncertainty, since the two metrics do not
always align; (2) include high-impact corruptions such as snow and zoom
blur in robustness testing; (3) conduct task-specific evaluation because
perception-related ADS tasks are more sensitive to corruptions; (4)
treat low uncertainty under corruptions cautiously, as it may indicate
overconfident wrong predictions; and (5) select LVLMs by considering the
trade-off among robustness, uncertainty, inference cost, and hardware
requirements, rather than accuracy alone. This addition clarifies how
our empirical findings can inform practical LVLM evaluation and adoption
in ADS scenarios.

---
- **Review B - Q1**: Clarify whether entropy measures sampled answer
inconsistency, not full LVLM uncertainty.
- **Response**: We will clarify in the next revision that prediction uncertainty
reflects output-level variability across sampling runs, capturing
predictive confidence rather than full LVLM uncertainty [2].

- **Review B - Q2**: Clarify how howGPT-4o-generated answer choices were
validated for ambiguity or label errors.
- **Response**: Our writing was unclear. NuPlanQA-Eval is the evaluation benchmark
from NuPlanQA [3]. All GPT-4o-generated choices have been manually
reviewed. We also followed the official benchmark guidelines and
re-checked all data after applying corruptions. We will clarify this in
the revised manuscript.

---
- **Review C - Q1**: Clarify how the evaluated VLM tasks can be
incorporated into full-stack ADSs, and the usefulness of the findings.
- **Response**: Thank you for the comment. We will clarify that the evaluated VLM
tasks can be incorporated into full-stack ADSs as auxiliary perception,
scene understanding, and decision-support modules, e.g., for traffic
light/key object recognition, traffic flow understanding, situation
assessment, maneuver reasoning, and action recommendation. We also added
that our findings help identify corruption-sensitive tasks, guide
uncertainty-aware validation, and inform robustness-resource trade-offs
when selecting LVLMs for ADS integration. See our response to Review A -
Q2 for more details.


- **Review C - Q2**: Clarify what actionable insights ADS developers can
learn from this study.
- **Response**: Thank you for the suggestion. We will clarify the actionable insights
for ADS developers and added practical guidelines in the revised
manuscript (see our response to Review A - Q2). In brief, developers
should jointly consider accuracy and uncertainty, test VLMs under
high-impact corruptions, apply task-specific validation for
perception-heavy ADS tasks, be cautious of overconfident errors, and
select LVLMs by balancing robustness, uncertainty, and deployment cost.

---
# Other Responses
---
- **Review A**: Clarify the sufficiency of only using Shannon entropy over
multiple outputs.
- **Response**: We agree that a single metric cannot capture all aspects of LVLM
uncertainty. Under our black-box setting, internal states are
unavailable, so uncertainty must be estimated from repeated output
samples. Shannon entropy is then used to quantify the dispersion of the
resulting empirical answer distribution in a model-agnostic manner.
Prior work suggests that sampling-based uncertainty measures often show
similar trends in fixed-form QA tasks [2]. We will clarify this
distinction and discuss the limitation of using a single metric in the
paper.

---
- **Review B**: Clarify the evaluation of ranking stability.
- **Response**: We will add a stability analysis using 10 samples on a representative
subset of the benchmark. Specifically, we will compare the uncertainty
estimates and LVLM rankings obtained with 5 and 10 samples, and report
their ranking consistency. This additional analysis will help assess
whether our main conclusions are sensitive to the sampling budget.


- **Review B**: Clarify whether concatenated images adversely affect LVLMs
trained on different image layouts.
- **Response**: We conducted a preliminary experiment to examine the potential impact
of image concatenation. Results showed that image concatenation did not
adversely affect the evaluated LVLMs. We will clarify this design choice
in the revised manuscript and make the preliminary experiment data
publicly available in our repository.


- **Review B**: Rewording RQ4.
- **Response**: Nice suggestion! We will reword RQ4 as suggested: "Which LVLM is more
promising for ADS under this benchmark setting?"

---
- **Review C**: Clarify why focus on prediction uncertainty.
- **Response**: Thank you for the concern. We agree that uncertainty in LVLMs includes
multiple types, e.g., input uncertainty, reasoning uncertainty,
parameter uncertainty. In addition, quantifying uncertainty in LVLMs
remains a challenge [4]. Our work focuses on output-level prediction
uncertainty because it can be measured for black-box/open-source LVLMs
and directly reflects response stability under visual corruptions. We
will revise the manuscript to make this scope explicit, avoid
overclaiming, and note other uncertainty types as future work. Still,
prediction uncertainty provides actionable evidence of unstable or
overconfident LVLM behavior, which is useful for ADS validation.


- **Review C**: Clarify the realism of the added corruptions.
- **Response**: Thank you for the comment. We will clarify in Section 2.2 that our
corruptions are inspired by prior studies on evaluating ADS under
complex visual degradation conditions (e.g., [1][5]) and are
generated using the standard Python `imagecorruptions` library. These
controlled corruptions approximate common weather, illumination, and
blur-related visual degradations in ADS scenarios, while providing a
systematic and reproducible robustness test. We also acknowledge that
they are synthetic approximations rather than full physical simulations.


---
## References
[1] Yasin Almalioglu, Mehmet Turan, Niki Trigoni, and Andrew Markham. 2022. Deep learning-based robust positioning for all-weather autonomous driving. Nature machine intelligence 4, 9 (2022), 749–760. https://doi.org/10.1038/s42256-022-00520-5

[2] Xiaoou Liu, Tiejin Chen, Longchao Da, et al . 2025. Uncertainty Quantification and Confidence Calibration in Large Language Models: A Survey. In Proceedings of the 31st ACM SIGKDD Conference on Knowledge Discovery and Data Mining V.2 (KDD ’25). 6107–6117. https://doi.org/10.1145/3711896.3736569

[3] Sung-Yeon Park, Can Cui, Yunsheng Ma, et al . 2025. NuPlanQA: A Large-Scale Dataset and Benchmark for Multi-View Driving Scene Understanding in Multi-Modal Large Language Models. In Proceedings of the IEEE/CVF International Conference on Computer Vision (ICCV). 8066–8076. https://arxiv.org/abs/2503.12772

[4] Ola Shorinwa, Zhiting Mei, Justin Lidard, et al . 2025. A Survey on Uncertainty Quantification of Large Language Models: Taxonomy, Open Research Challenges, and Future Directions. ACM Comput. Surv. 58, 3, Article 63 (Sept. 2025), 38 pages. https://doi.org/10.1145/3744238

[5] Shaoyuan Xie, Lingdong Kong, Yuhao Dong, et al . 2025. Are VLMs Ready for Autonomous Driving? An Empirical Study from the Reliability, Data and Metric Perspectives. In Proceedings of the IEEE/CVF International Conference on Computer Vision. 6585–6597. https://arxiv.org/abs/2501.04003

[6] Xingcheng Zhou, Mingyu Liu, Ekim Yurtsever, et al . 2024. Vision Language Models in Autonomous Driving: A Survey and Outlook. IEEE Transactions on Intelligent Vehicles (2024), 1–20. https://doi.org/10.1109/TIV.2024.3402136




