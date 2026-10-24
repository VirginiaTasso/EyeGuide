# Knowledge Distillation for Fundus Image Classification

This project proposes a **knowledge distillation** framework for improving CNN performance in characterizing eye cancer by transferring knowledge from a teacher model trained on more informative, lesion-centered images to a student model operating on full-field fundus images.

## Project Overview

## Publication

A detailed description of the methodology and experimental results can be found in the **EMBC 2026 paper**:

[Transferring lesion-centered representations to full-field fundus images for robust classification of uveal melanocytic lesions](https://www.research.ed.ac.uk/en/publications/transferring-lesion-centered-representations-to-full-field-fundus/)

## Directory Structure

```text
knowledge_distillation/
├── src/
│   ├── main.py                      # Main training script with knowledge distillation pipeline
│   ├── zoom_experiment.py           # Experiment script for evaluating zoom/dilation levels
│   └── utils/
│       ├── dataset.py               # Dataset classes (FundusClsDataset, FundusClsDatasetZoom, PairedFundusDataset)
│       ├── model.py                 # Model architectures (ResNet18, VGG16, ViT, Swin classifiers)
│       ├── training.py              # Training and testing functions
│       ├── losses.py                # Knowledge distillation loss functions
│       ├── transforms.py            # Transforms
│       ├── metrics.py               # Evaluation metrics
│       ├── visualization.py         # Visualization and logging utilities
│       ├── seed.py                  # Random seed
│       └── generals.py              # General utility functions
├── config/
│   └── config.yaml                  # Hydra configuration file
├── models/                          # Directory for saved model checkpoints
├── exec.sh                          # Docker execution script
└── README.md
```

## Configuration

The training pipeline is configured via `config/config.yaml`. Key parameters include:

```yaml
# Model & Training
n_epochs: 500
batch_size: 16
RANDOM_SEED: 42

# Knowledge Distillation
temperature: 3.0
beta: 0.5
soft_w: 0.75
ce_w: 0.25

# Data Augmentation
dilation_percentage: 1.0

# Paths
base_dir: /home/virginia/PerspectiveStudy
data_dir: /home/virginia/EyeCancerDetection
csv_file: fundus_data_final.csv

# Training Configuration
teacher_lr: 1e-4
student_lr: 1e-4
weight_decay: 1e-4
patience: 30
```

## Usage

### Basic Training with Knowledge Distillation

```bash
python src/main.py
```

This will:
1. Load the fundus image dataset from configured paths.
2. Train a teacher model on the full dataset.
3. Train a student model using knowledge distillation from the teacher.
4. Save models, logs, and results to the specified directories.

---

**Last Updated**: October 2026
