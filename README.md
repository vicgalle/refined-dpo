# Refined Direct Preference Optimization (rDPO)

Code for the paper "Refined Direct Preference Optimization with Synthetic Data for Behavioral Alignment of LLMs", under review at ICLR 2024 Re-Align Workshop.

> In this paper, we introduce refined Direct Preference Optimization
(rDPO), a method for improving the behavioral alignment of Large Language
Models (LLMs) without the need for human-annotated data. The method involves
creating synthetic data using self-critique prompting by a teacher LLM and then
utilising a generalized DPO loss function to distil to a student LLM. The loss
function incorporates an additional external reward model to improve the
quality of synthetic data, making rDPO robust to potential noise in the
synthetic dataset. rDPO is shown to be effective in a diverse set of
behavioural alignment tasks, such as improved safety, robustness against
role-playing, and reduced sycophancy.

## 1. Data Generation

We use the Mixtral 8x7B model through the Together API at https://www.together.ai, so you will need an API token.

You can run the following notebook to generate synthetic data:

```bash
generate_data.ipynb
```

where `generate_data.ipynb` is located in each of the three experiment folders from the paper:

* `safety`: avoiding generating harmful responses.


Inside each `generate_data.ipynb` file, you will find the exact prompts for each experiment, in particular:

* The original prompt for each example.
* The critique prompt.
* The review prompt.


## Model Distillation (SFT)

Once you have generated the synthetic data, you can finetune the model over a training split of the synthetic data. You may filter the data first using the reward scores of the revised and original sample (acceptance step in the paper). This is recommended as it improves the results over the test set of prompts.

Run the notebook [`run_distillation.ipynb`](run_distillation.ipynb) to self-distil the model on the synthetic data generated in the previous seep. The notebook uses the `sentiment` task an example, but it can be easily adapted to the other tasks.

### Citation

If you find this work useful, please consider citing with

```
@misc{gallego2023distilled,
      title={Distilled Self-Critique of LLMs with Synthetic Data: a Bayesian Perspective}, 
      author={Victor Gallego},
      year={2023},
      eprint={2312.01957},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
```
