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
* `roleplay-robustness`: robustness against role-playing injection in the user prompt.
* `sycophancy`: avoid being biased by the user when providing feedback.


Inside each `generate_data.ipynb` file, you will find the exact prompts for each experiment, in particular:

* The original prompt for each example.
* The critique prompt.
* The review prompt.


## 2. Data scoring

To score the previous synthetic data using the external reward model, just execute the following notebook configuring the paths inside:

```bash
reward_score.ipynb
```

Again, the notebook is located in each of the three experiment folders. It will add keys with the scores for each example in the dataset. Also, in those notebooks you can find the prompt template used to evaluate with the reward model.



## 3. Student model distillation with rDPO

Code will be uploaded soon!
