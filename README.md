# Drug Powder Uniformity Dataset

A microscopic image dataset developed for deep-learning-based classification of pharmaceutical powder mixing uniformity.

## Overview

The **Drug Powder Uniformity Dataset** is intended to support research on automated assessment of pharmaceutical powder mixing using computer vision and deep learning. The dataset contains microscopic images organized into training, validation, and testing subsets.

The classification task focuses on distinguishing between:

- **Mixed:** Powder samples exhibiting characteristics associated with adequate mixing.
- **Not Mixed:** Powder samples exhibiting characteristics associated with inadequate or non-uniform mixing.

This dataset can be used to investigate image classification models, data augmentation strategies, feature extraction, and explainable artificial intelligence for pharmaceutical process monitoring.

## Dataset Structure

```text
drug-powder-uniformity-dataset/
├── Testing/
│   └── Image files
├── Training/
│   ├── Mixed/
│   │   └── Image files
│   └── Not Mixed/
│       └── Image files
└── Validation/
    ├── Mixed/
    │   └── Image files
    └── Not Mixed/
        └── Image files
```

**Note:** The Testing directory currently contains 140 images. The Training and Validation directories contain class-specific subfolders.

## Intended Applications

- Pharmaceutical powder mixing uniformity assessment
- Microscopic image classification
- Deep learning and computer vision research
- Comparison of CNN-based classification architectures
- Data augmentation and model generalization studies
- Explainable AI for pharmaceutical image analysis
- Potential applications in pharmaceutical process monitoring

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/abhicse8379/drug-powder-uniformity-dataset.git
```

### 2. Navigate to the Dataset

```bash
cd drug-powder-uniformity-dataset
```

### 3. Install Dependencies

For PyTorch-based experiments, install the required packages:

```bash
pip install torch torchvision matplotlib scikit-learn pillow
```

Installation requirements may vary depending on the model and computing environment.

## Loading the Dataset with PyTorch

The following example loads the Training and Validation directories using `ImageFolder`.

```python
from torchvision import datasets, transforms
from torch.utils.data import DataLoader

data_dir = "."

transform = transforms.Compose([
    transforms.Resize((224, 224)),
    transforms.ToTensor()
])

train_dataset = datasets.ImageFolder(
    root=f"{data_dir}/Training",
    transform=transform
)

val_dataset = datasets.ImageFolder(
    root=f"{data_dir}/Validation",
    transform=transform
)

train_loader = DataLoader(
    train_dataset,
    batch_size=32,
    shuffle=True
)

val_loader = DataLoader(
    val_dataset,
    batch_size=32,
    shuffle=False
)

print("Class mapping:", train_dataset.class_to_idx)
print("Training images:", len(train_dataset))
print("Validation images:", len(val_dataset))
```

**Important:** This example assumes that the Training and Validation directories contain the two class folders shown above. The class mapping is determined automatically by `ImageFolder`.

## Dataset Statistics

The Drug Powder Uniformity Dataset contains **1,731 microscopic images** distributed across training, validation, and testing subsets.

| Dataset Split | Mixed | Not Mixed | Total Images |
|---|---:|---:|---:|
| Training | 548 | 633 | 1,181 |
| Validation | 192 | 218 | 410 |
| Testing | Not specified | Not specified | 140 |
| **Total** | **740*** | **851*** | **1,731** |

*Note: The Mixed and Not Mixed totals include only the labeled Training and Validation subsets. The 140 Testing images have not been separated by class in the reported statistics.*

### Dataset Distribution

- **Training set:** 1,181 images
  - Mixed: 548 images
  - Not Mixed: 633 images
- **Validation set:** 410 images
  - Mixed: 192 images
  - Not Mixed: 218 images
- **Testing set:** 140 images

The dataset is designed for developing and evaluating deep-learning models for pharmaceutical powder mixing uniformity classification. The class distribution and image labels should be verified before training and final evaluation.

Only do this when the correct ground-truth labels are available. If the images are unlabeled, use a custom dataset loader instead.

## Suggested Research Workflow

1. Inspect the dataset and verify image labels.
2. Check the distribution of samples across classes and subsets.
3. Apply suitable preprocessing and training-only data augmentation.
4. Train and validate CNN-based image classification models.
5. Evaluate the final model using the held-out test set.
6. Report accuracy, precision, recall, F1-score, and confusion matrix.
7. Consider Grad-CAM or other explainability techniques to analyze model predictions.

## Important Considerations

- Keep the test set separate from training and model selection.
- Avoid data leakage between training, validation, and testing.
- Ensure that images originating from the same physical sample or acquisition session are assigned appropriately to prevent overly optimistic evaluation.
- Report dataset size, class distribution, preprocessing, and experimental limitations transparently.
- Classification results should not be interpreted as proof of pharmaceutical content uniformity without appropriate experimental validation.

## Citation

If you use this dataset in research, please cite the repository URL:

Abhishek Patel, *Drug Powder Uniformity Dataset*, GitHub repository: https://github.com/abhicse8379/drug-powder-uniformity-dataset

A formal citation can be added when a DOI or associated publication becomes available.

## License

A license has not yet been specified. Please add an appropriate license before permitting redistribution or reuse. Ensure that you have the necessary rights to share the images.

## Disclaimer

This dataset is intended for research and educational purposes. It is not, by itself, a validated pharmaceutical quality-control method or a substitute for appropriate laboratory testing and regulatory requirements.

## Contact

For research-related questions, please contact the repository maintainer through GitHub.
