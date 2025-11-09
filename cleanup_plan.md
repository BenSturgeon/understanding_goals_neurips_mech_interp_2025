# Paper Repo Cleanup Plan

## Files to DELETE (Visualization & Testing - 14 files)

### Feature Visualization (12 files)
- src/custom_feature_visualisation.py
- src/feature_vis_decorrelated.py
- src/feature_vis_impala.py
- src/feature_vis_sae.py
- src/feature_vis_sweep.py
- src/feature_visualisation.py
- src/run_original_layer_visualization.py
- src/run_sae_visualization.py
- src/utils/activation_steering_visualisations.py
- src/visualisation_functions.py
- src/visualise_sae_activations.py
- src/visualize_max_activations.py

### Test/Debug Files (2 files)
- src/test_lucent.py
- src/test_zero_activation_bias.py

### Color Decorrelation (1 file - not used in paper)
- src/color_decorrelation.py
- src/visualise_decorrelated.ipynb

## Files to KEEP - Core Paper Code

### ROOT LEVEL (3 files)
- generate_viable_seeds.py ✓ (user specified)
- requirements.txt
- setup.py

### Experiments (8 files)
- src/quantitative_intervention_experiment.py
- src/quantitative_intervention_experiment_batched.py ✓ (user specified)
- src/channel_ablatation_experiments.py
- src/channel_ablation_sweep.py
- src/zero_ablation_classes.py
- src/zero_ablation_experiment.py
- src/parallel_ablation_sweep.py
- src/sequential_intervention_experiment.py

### Interventions (5 files)
- src/intervention_base.py
- src/direct_intervention.py
- src/base_model_intervention.py
- src/run_direct_intervention.py
- src/parallel_quantitative_intervention.py

### SAE (6 files)
- src/sae.py
- src/sae_cnn.py
- src/sae_training.py
- src/sae_xla.py
- src/sae_spatial_intervention.py
- src/run_sae_intervention.py

### Analysis (5 files)
- src/analyze_activations.py
- src/plot_ablation_results.py
- src/plot_entity_distribution.py
- src/perform_sae_analysis.py
- src/discover_sae_directions.py
- src/extract_sae_features.py

### Utilities (4 files)
- src/utils/helpers.py
- src/utils/heist.py
- src/utils/create_intervention_mazes.py
- src/utils/environment_modification_experiments.py

### Models (4 files)
- src/interpretable_impala.py
- src/interpretable_impala_no_dropout_envpool.py
- src/impala_dropout.py
- src/policies_impala.py

### Maze/Environment (2 files)
- src/bias_corrected_mazes.py
- src/track_object_channels.py
- src/track_base_model_channels.py
- src/run_base_model_serial_experiments.py
- src/run_ablation_serial_experiments_optimal_bias.py

### Probing (1 file)
- src/probing.py

### Training (1 file)
- src/train_procgen_wandb.py

### Other (1 file)
- src/detect_dead_channels.py

## Summary
- DELETE: 17 files (visualization + tests)
- KEEP: ~40 files (core experiments)
- Total reduction: ~30% fewer files

