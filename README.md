# Causal inference: graphs, adjustment, and measurement error

An independent educational project by Edderic Ugaddan combining explanatory notebooks, simulated data, and Python implementations. The central question is: **when can observational data tell us what would happen under an intervention?**

## Start with these notebooks

| Notebook | Question and methods |
| --- | --- |
| [Introduction to Causal Inference: Part 1](intro-to-ci-part-1.ipynb) | Why can a beneficial treatment look harmful in observational data? Uses a simulated tutoring/graduation example, DAGs, the backdoor criterion, and the adjustment formula (g-formula) to estimate a population-average causal risk difference. |
| [Measurement Error in Causal Inference](measurement-error/measurement-error.ipynb) | What happens when a confounder is latent and only a proxy is observed? Explores a synthetic socioeconomic-status/tutoring/graduation model with PyMC3, prior predictive sampling, and posterior inference. |

These are teaching and modeling experiments using synthetic data, rather than analyses of actual student or patient treatment outcomes.

## Treatment-effect estimation example

The introductory notebook constructs a known data-generating process in which at-risk students are more likely to receive tutoring and less likely to graduate. It compares:

1. The unadjusted difference in graduation rates between treated and untreated students.
2. An idealized randomized-treatment simulation.
3. An observational estimate using `prob_grad_do`, which standardizes stratum-specific outcomes over the population distribution of risk.

For this example, the adjustment is:

```text
E[G | do(T=t)] = sum_r E[G | T=t, R=r] P(R=r)
Average treatment effect = E[G | do(T=1)] - E[G | do(T=0)]
```

The causal interpretation depends on the assumed graph and identification conditions, including consistency, adequate treatment overlap, and adjustment for the relevant confounder. The notebook also explains chains, forks, colliders, descendants of colliders, selection bias, and intervention notation.

## Bayesian measurement-error experiment

The second notebook generates synthetic socioeconomic status, tutoring, graduation, and a free/reduced-lunch proxy. It explores models where the confounder is observed versus latent, and compares model parameters and intervention-based outcome contrasts.

The experiment supplies the data-generating structure and informative priors centered on known simulation parameters. It is an exploratory demonstration, not evidence that a proxy alone identifies a causal effect in an arbitrary observational dataset. The notebook retains TODOs and unfinished analysis; its effect summaries require further review before use for substantive inference.

## Reading and running

The notebooks can be read directly on GitHub. For local exploration, the repository includes a historical Conda environment:

```bash
conda env create -f environment.yml
conda activate causal-inf-experiments
jupyter notebook
```

The environment pins older NumPy/pandas/PyMC3/Theano versions and may need a compatible platform or migration. It has not been recreated for this documentation update.

Before executing the introductory notebook, reduce `sample_size = 100000000` to a smaller value, such as `100000`, to limit memory use. Estimates will have more Monte Carlo variation. Some narrative values and formulas contain inconsistencies; use the actual simulation parameters and code when checking numerical results. External image links may also have aged.

## Related work

- [Bayesian Python examples for *Causal Inference*](https://github.com/Edderic/causal-inference-python-bayesian): textbook-based outcome regression and posterior uncertainty.
- [Causal discovery](https://github.com/Edderic/causal_discovery): conditional-independence testing, graph algorithms, and missing-data experiments.
