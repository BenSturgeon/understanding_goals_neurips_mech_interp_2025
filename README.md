# Understanding Goals in a Maze Solving Agent

**NeurIPS 2025 Mechanistic Interpretability Workshop**

📄 [Paper (OpenReview)](https://openreview.net/forum?id=KwxgxWsjE3) | 💾 [Model Files (Google Drive)](https://drive.google.com/drive/folders/1zfp0aQ-1SquHTpJFoq8k9SsyQ80CgCWm?usp=sharing)

## Abstract

This repository contains the code to reproduce experiments from our paper on understanding goal representations in a maze-solving agent trained on the Procgen Heist environment. We use channel ablation and quantitative intervention experiments to identify "infrastructure channels" that represent critical game state (e.g., which keys have been collected) and demonstrate their causal influence on navigation decisions.

## Key Findings

- **Infrastructure Channels**: Specific CNN channels cleanly represent game state (key collection status)
- **Causal Influence**: These channels directly affect the agent's goal-directed navigation
- **Interpretable Representations**: Channel ablations reveal interpretable features rather than polysemantic encodings
- **SAE Validation**: Sparse autoencoders confirm our findings and provide additional decomposition



## Repository Structure

```
src/
├── Experiments/
│   ├── quantitative_intervention_experiment.py       # Main intervention experiments
│   ├── quantitative_intervention_experiment_batched.py
│   ├── channel_ablatation_experiments.py            # Channel ablation studies
│   ├── zero_ablation_experiment.py                  # Baseline measurements
│   └── sequential_intervention_experiment.py
│
├── SAE/
│   ├── sae_cnn.py                                   # SAE architecture
│   ├── sae_training.py                              # Training pipeline
│   └── sae_spatial_intervention.py                  # SAE-based interventions
│
├── Interventions/
│   ├── intervention_base.py                         # Base framework
│   ├── direct_intervention.py                       # Direct channel manipulation
│   └── base_model_intervention.py                   # Model-level interventions
│
├── Analysis/
│   ├── analyze_activations.py                       # Activation statistics
│   ├── plot_entity_distribution.py                  # Entity distribution plots
│   └── plot_ablation_results.py                     # Ablation visualizations
│
└── Utils/
    ├── helpers.py                                   # Model loading utilities
    ├── heist.py                                     # Procgen environment wrappers
    └── create_intervention_mazes.py                 # Custom maze generation
```

## Prerequisites
- Python 3.9 (specific version required)
- Qt5 (for macOS users)
- Git

## Installation
### Option 1: Using a script (Recommended for Speed)

We provide an automated setup script to install all dependencies, configure your environment, and prepare everything for running experiments:

This is designed for running on a remote linux machine and includes steps for generating an ssh key and installing procgen and procgen-tools from source.

It uses UV and will install it automatically. It will also install QT5 which is a necessary dependency for building Procgen. This is needed on both mac and Linux.

```bash
chmod +x automated_setup.sh

./automated_setup.sh
```

### Option 2: Manual installation using uv 

# Install uv if you haven't already
pip install uv

# Create virtual environment with Python 3.9
uv venv --python=3.9

# Activate the environment
source .venv/bin/activate

# Install dependencies
uv pip install -r requirements.txt

# Install procgen from source (required)
git clone https://github.com/openai/procgen.git
cd procgen
uv  pip install -e .


# Install procgen tools from source (required)
git clone https://github.com/UlisseMini/procgen-tools
cd procgen-tools
uv -m pip install -e .


## macOS Setup
macOS users need to install Qt5 before building procgen:

```bash
# Install Qt5
brew install qt@5

# Add Qt to your PATH (add this to your ~/.zshrc or ~/.bashrc)
export PATH="/usr/local/opt/qt@5/bin:$PATH"
```

## Known Issues and Solutions

### Procgen Build Issues
If you encounter build errors with procgen, modify `CMakeLists.txt` in the procgen source:
```cmake
# Find this line:
# add_compile_options(-Wextra -Wshadow -Wall -Wformat=2 -Wundef -Wvla -Wmissing-include-dirs -Wnon-virtual-dtor -Werror)

# Replace it with:
add_compile_options(-Wextra -Wshadow -Wall -Wformat=2 -Wundef -Wvla -Wmissing-include-dirs -Wnon-virtual-dtor -Wno-unused-parameter -Wno-unused-variable)
```

### Environment Issues
- Always use `python -m pip` instead of just `pip` when not using uv or poetry
- Verify your environment is correct:
```bash
which python
python --version  # should show Python 3.9.x
```

### Version Conflicts
- Use a fresh virtual environment if you encounter persistent issues
- Make sure procgen is installed before procgen-tools
- Verify you're using Python 3.9

## Verifying Installation
After installation, verify everything works:
```python
python
>>> import procgen_tools
>>> import procgen
```

## Model Files

Download the pre-trained model checkpoints and SAE weights from [Google Drive](https://drive.google.com/drive/folders/1zfp0aQ-1SquHTpJFoq8k9SsyQ80CgCWm?usp=sharing):

- `64_256_8_36001_0.pt` - IMPALA model checkpoint at step 35k (1.4 MB)
- `conv3a/sae_checkpoint_step_2000000.pt` - SAE for conv3a layer (105 KB)
- `conv4a/sae_checkpoint_step_2000000.pt` - SAE for conv4a layer (105 KB)

Place the downloaded files in the appropriate directories:
```bash
mkdir -p base_models new_saes/conv3a new_saes/conv4a
mv 64_256_8_36001_0.pt base_models/
mv conv3a_sae_checkpoint_step_2000000.pt new_saes/conv3a/sae_checkpoint_step_2000000.pt
mv conv4a_sae_checkpoint_step_2000000.pt new_saes/conv4a/sae_checkpoint_step_2000000.pt
```

## Reproducing Paper Experiments

### Main Quantitative Intervention Experiments (Section 3)

```bash
python src/quantitative_intervention_experiment_batched.py
```

### Channel Ablation Studies (Section 4)

```bash
python src/channel_ablatation_experiments.py
python src/zero_ablation_experiment.py
```

### SAE Training and Validation (Section 5)

Train SAEs on conv3a and conv4a layers:
```bash
python src/sae_training.py --layer conv3a
python src/sae_training.py --layer conv4a
```

Run SAE interventions:
```bash
python src/sae_spatial_intervention.py
```

### Generating Figures

```bash
python src/plot_entity_distribution.py
python src/plot_ablation_results.py
python src/analyze_activations.py
```

## Citation

If you use this code or build upon our work, please cite:

```bibtex
@inproceedings{sturgeon2025understanding,
  title={Understanding Goals in a Maze Solving Agent},
  author={Sturgeon, Ben and others},
  booktitle={NeurIPS 2025 Workshop on Mechanistic Interpretability},
  year={2025},
  url={https://openreview.net/forum?id=KwxgxWsjE3}
}
```

## License

[To be added]

## Contact

For questions or issues, please open an issue on GitHub.
