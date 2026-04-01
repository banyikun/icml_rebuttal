


 Caption: We cannot perform large-scale parallel sampling and voting in the same way as standard TTS. As a compromise, we compared the major@64 performance of SAGE-RL-tuned DS-1.5B with DeepConf (budget=64, warm_up=4) on AIME 2024   ("spp"， **s**econds **p**er **p**rompt).


| Model                          | pass@1 | pass@64 | major@64 | spp  |
|--------------------------------|--------|--------|---------|------|
| **DS-1.5B**                       |   25.1     |  73.3  |   46.7      | 333.9     |
| +DeepConf                     |    -    |    -    |    53.3     | 243.8      | 
| **SAGE-GRPO-DS-1.5B**                       |    28.8    |    76.7    |    56.7     |   192.4   |
| +DeepConf              |   -    |    -    |   63.3     |  152.3    |

