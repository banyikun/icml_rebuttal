
Since SAGE performs branching search starting from the same prefix and ultimately returns only a limited number of sequences, we cannot perform large-scale parallel sampling and voting in the same way as standard TTS. As a compromise, we compared the major@64 performance of SAGE-RL-tuned DS-1.5B with DeepConf (budget=64, warm_up=4) on AIME 2024.

Specifically, for methods other than DeepConf, we repeated each prompt 64 times on AIME 2024. For pass@k, a prompt is considered correct if any of the 64 responses contains the correct answer. For major@k, we evaluate the correctness of the majority vote among the 64 responses. In contrast, DeepConf samples 64 responses per prompt, among which 4 responses are used to compute the threshold. If the termination mechanism is triggered, sampling stops early. The final answer is returned via confidence-weighted voting, and we report this result as major@64.


The experimental results are shown below, where "spp" reports the average processing time per prompt (**s**econds **p**er **p**rompt).


| Model                          | pass@1 | pass@64 | major@64 | spp  |
|--------------------------------|--------|--------|---------|------|
| **DS-1.5B**                       |   25.1     |  73.3  |   46.7      | 333.9     |
| +DeepConf                     |    -    |    -    |    53.3     | 243.8      | 
| **SAGE-GRPO-DS-1.5B**                       |    28.8    |    76.7    |    56.7     |   192.4   |
| +DeepConf              |   -    |    -    |   63.3     |  152.3    |

DeepConf not only significantly improves the major@64 of DS-1.5B, but also leads to a substantial reduction in spp. As a completely training-free method, the improvement in major@64 primarily comes from confidence-based majority voting, while the reduction in spp is mainly attributed to threshold-based early pruning. 

Meanwhile, SAGE-RL achieves a slightly higher major@64 than DeepConf while obtaining a noticeably lower spp. This improvement mainly stems from the transformation of the model’s own reasoning pattern, enabling the policy model to intrinsically select more precise reasoning paths during inference.


Additionally, we found that SAGE performs exceptionally well under the majority voting metric. Compared to pass@1 (+3.7%) and pass@64 (+3.4%), the improvement in major@64 (+10.0%) is particularly significant. 
Surprisingly, when we applied DeepConf on SAGE-GRPO-DS-1.5B, the major@64 reached a remarkable 63.3%. This indicates that internalizing the high-confidence and efficient reasoning pattern into the model parameters brings substantial gains in majority-voting scenarios.
