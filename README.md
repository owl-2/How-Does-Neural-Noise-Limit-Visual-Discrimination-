# How Does Neural Noise Limit Visual Discrimination?

### A computational study of orientation tuning, neural population coding, and sensory information

## Overview

How does the brain distinguish between two visual stimuli that are very similar?

Individual neurons do not produce exactly the same response every time they encounter a stimulus. Their spike counts vary across repeated presentations, and activity across neurons can also fluctuate together.

This project uses computational simulations to investigate how neuronal response variability influences the representation and discrimination of visual orientation.

Using a simplified population of orientation-selective neurons, I explored how tuning properties, Poisson spike-count variability, population size, and shared fluctuations influence the information available about a visual stimulus.

The project connects individual neuronal responses to population-level sensory coding and the theoretical limits of stimulus estimation.

**This is a computational modelling project using simulated neural responses, not experimental neural recordings or human behavioural data.**

## Research questions

- How does an orientation-selective neuron respond to different visual orientations?
- How does Poisson spike-count variability affect the discrimination of nearby orientations?
- Can a population of differently tuned neurons improve stimulus discrimination?
- How do shared trial-to-trial fluctuations produce correlations between neuronal responses?
- How does Fisher information relate to the theoretical precision of sensory estimation?

## Computational approach

### 1. Orientation tuning

Modelled orientation-selective neurons using Gaussian-shaped tuning curves.

Each neuron has a preferred orientation, baseline firing rate, response amplitude, and tuning width.

### 2. Poisson spike-count variability

Converted mean firing rates into expected spike counts and simulated repeated neuronal responses using Poisson distributions.

This allowed comparison of response distributions for two nearby orientations: **20° and 25°**.

### 3. Single-neuron decoding

Implemented a maximum-likelihood decoder to estimate which of the two candidate orientations most likely produced an observed spike count.

The simulated single-neuron balanced accuracy was approximately **52%**.

### 4. Population coding and decoding

Extended the model to a population of three neurons with different preferred orientations.

Implemented population maximum-likelihood decoding under independent Poisson responses.

Also used a nearest-mean decoder to compare discrimination under independent and shared-gain noise conditions.

### 5. Shared-gain fluctuations and correlated responses

Introduced a positive, trial-specific gain fluctuation shared across neurons.

This creates correlated neuronal responses while preserving the mean response under the specified gain model.

Compared response correlations and decoding performance between independent and shared-gain conditions.

### 6. Population size and discrimination

Varied the population size from 1 to 24 neurons, distributing preferred orientations between 5° and 35°.

Investigated how population size influences balanced decoding accuracy under independent and shared-gain noise.

### 7. Fisher information and estimation precision

Calculated single-neuron and population Fisher information.

Used the Cramér–Rao lower bound (CRLB) to examine the theoretical relationship between Fisher information and the precision of orientation estimation.

### 8. Fisher information under correlated noise

Calculated population Fisher information using a Gaussian moment approximation for the shared-gain response model.

This approximation includes information carried by changes in both the mean response and the covariance structure.

It is not the exact Fisher information of the underlying Poisson-lognormal mixture.

## Selected simulation results

### Visual orientation discrimination

The model compares two nearby orientations: 20° and 25°.

| Model | Balanced decoding accuracy |
|---|---:|
| Single neuron | 52.0% |
| Three-neuron population, independent noise | 60.4% |
| Three-neuron population, shared-gain noise | 60.7% |

### Effect of population size

| Number of neurons | Independent noise | Shared-gain noise |
|---:|---:|---:|
| 1 | 59.3% | 56.4% |
| 3 | 61.3% | 59.9% |
| 6 | 65.8% | 66.7% |
| 12 | 72.6% | 71.7% |
| 24 | 80.1% | 78.0% |

Decoding accuracy generally increased with population size in this simulation.

The small differences between independent and shared-gain conditions illustrate that correlations do not necessarily produce the same effect on decoding accuracy across all population sizes and model conditions.

### Fisher information and CRLB

For the three-neuron population at 20°:

| Measure | Independent Poisson | Shared-gain Gaussian approximation |
|---|---:|---:|
| Fisher information | 0.01114 degree⁻² | 0.01859 degree⁻² |
| CRLB standard deviation | 9.48° | 7.33° |

These values come from different statistical calculations: exact Fisher information for the independent Poisson model and an approximate Gaussian calculation for the shared-gain model. They should not be interpreted as direct evidence that correlated noise improves perception.

## Key concepts explored

- Orientation-selective neuronal tuning
- Gaussian tuning curves
- Poisson spike-count distributions
- Neural response variability
- Population coding
- Maximum-likelihood decoding
- Nearest-mean classification
- Shared gain fluctuations
- Noise correlations
- Fisher information
- Cramér–Rao lower bound
- Gaussian approximation of correlated responses

## Tools and libraries

- Python
- NumPy
- SciPy
- Matplotlib
- Pandas
- Jupyter Notebook

## Repository structure

```text
neural-noise-visual-discrimination/
│
├── neural_noise_visual_discrimination_project_updated.ipynb
└── README.md
```

## How to run

1. Clone or download this repository.
2. Install the required Python libraries.
3. Open the notebook using Jupyter Notebook or JupyterLab.
4. Run the cells sequentially from beginning to end.

Install dependencies:

```bash
pip install numpy scipy matplotlib pandas jupyter
```

The notebook uses a fixed NumPy random seed for reproducibility when executed in order.

## Model assumptions and limitations

This project uses simplified models to explore principles of sensory coding.

Important limitations include:

- Neuronal orientation tuning is represented using Gaussian functions.
- Spike counts follow Poisson distributions, assuming conditional variance equals the mean.
- Shared gain is used as a simplified mechanism for generating positive response correlations.
- The nearest-mean decoder is not guaranteed to be optimal.
- Discrimination is evaluated using only two candidate orientations.
- Preferred-orientation arrangements
