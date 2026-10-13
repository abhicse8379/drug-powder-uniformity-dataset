# Drug Powder Uniformity Dataset

**A Microscopic Image Dataset for Deep Learning-Based Pharmaceutical Powder Mixing Uniformity Classification**

[![Dataset](https://img.shields.io/badge/Dataset-Microscopic%20Images-blue)](https://github.com/abhicse8379/drug-powder-uniformity-dataset)
[![Task](https://img.shields.io/badge/Task-Binary%20Classification-green)](https://github.com/abhicse8379/drug-powder-uniformity-dataset)
[![Framework](https://img.shields.io/badge/Framework-PyTorch-red)](https://pytorch.org/)

## Overview

The **Drug Powder Uniformity Dataset** is a microscopic image dataset intended to support research on automated pharmaceutical powder mixing uniformity assessment using computer vision and deep learning.

The dataset is organized into training, validation, and testing subsets and is intended for binary image classification. The classification task distinguishes between powder samples labeled **Mixed** and **Not Mixed**.

Automated microscopic image analysis may help investigate computer vision-based approaches for pharmaceutical process monitoring, in-process quality control, and the assessment of powder mixing characteristics.

This repository provides the dataset organization and a basic PyTorch loading example to help researchers get started with model development and evaluation.

## Dataset at a Glance

| Attribute | Description |
|---|---|
| Dataset name | Drug Powder Uniformity Dataset |
| Data modality | Microscopic images |
| Application domain | Pharmaceutical powder mixing |
| Machine learning task | Binary image classification |
| Classes | Mixed, Not Mixed |
| Total reported images | 1,731 |
| Training images | 1,181 |
| Validation images | 410 |
| Testing images | 140 |
| Deep learning framework | PyTorch |
| Repository | [GitHub](https://github.com/abhicse8379/drug-powder-uniformity-dataset) |

## Classification Categories

### 1. Mixed

Images assigned to the Mixed category represent powder samples labeled as adequately or uniformly mixed according to the dataset's labeling protocol.

### 2. Not Mixed

Images assigned to the Not Mixed category represent powder samples labeled as inadequately mixed or non-uniform according to the dataset's labeling protocol.

**Important:** These categories represent dataset labels. Model predictions alone do not establish pharmaceutical content uniformity, drug concentration, or regulatory compliance.

## Dataset Structure

```text
drug-powder-uniformity-dataset/
├── Testing/
│   └── Image files (140)
│
├── Training/
│   ├── Mixed/
│   │   └── Image files (548)
│   └── Not Mixed/
│       └── Image files (633)
│
└── Validation/
    ├── Mixed/
    │   └── Image files (192)
    └── Not Mixed/
        └── Image files (218)
```

The Testing directory is currently reported to contain 140 images directly. Class-specific counts for these images have not been provided.

## Dataset Statistics

The dataset contains **1,731 reported microscopic images** across three subsets.

| Dataset Split | Mixed | Not Mixed | Total |
|---|---:|---:|---:|
| Training | 548 | 633 | 1,181 |
| Validation | 192 | 218 | 410 |
| Testing | --- | --- | 140 |
| **Total** | **740*** | **851*** | **1,731** |

*The class totals of 740 Mixed and 851 Not Mixed cover the Training and Validation subsets only. They exclude the 140 Testing images because their class distribution has not been reported.*

### Class Distribution

- **Training:** 46.4% Mixed and 53.6% Not Mixed.
- **Validation:** 46.8% Mixed and 53.2% Not Mixed.

The training and validation subsets have relatively similar class distributions. Researchers should verify the labels and sample counts before conducting experiments.

## Intended Applications

This dataset may support research in the following areas:

- Microscopic pharmaceutical powder image classification
- Deep learning-based powder mixing assessment
- Convolutional neural network (CNN) architecture comparison
- Image preprocessing and data augmentation
- Transfer learning and feature extraction
- Model generalization and performance evaluation
- Explainable artificial intelligence (XAI), including Grad-CAM
- Research into computer vision-assisted pharmaceutical process monitoring

## Getting Started

### 1. Clone the Repository

Open a terminal and execute:

```bash
git clone https://github.com/abhicse8379/drug-powder-uniformity-dataset.git
cd drug-powder-uniformity-dataset
```

### 2. Create a Python Environment (Recommended)

```bash
python -m venv .venv
```

Activate the environment on Windows:

```powershell
.\.venv\Scripts\Activate.ps1
```

### 3. Install Dependencies

Install the packages required for the example:

```bash
pip install torch torchvision matplotlib scikit-learn pillow
```

For GPU training, install the PyTorch build compatible with your operating system and CUDA environment using the official [PyTorch installation guide](https://pytorch.org/get-started/locally/).

## Loading the Dataset with PyTorch

The following example loads the Training and Validation subsets using `torchvision.datasets.ImageFolder`.

```python
from pathlib import Path
from torchvision import datasets, transforms
from torch.utils.data import DataLoader

data_dir = Path(".")

transform = transforms.Compose([
    transforms.Resize((224, 224)),
    transforms.ToTensor()
])

train_dataset = datasets.ImageFolder(
    root=str(data_dir / "Training"),
    transform=transform
)

val_dataset = datasets.ImageFolder(
    root=str(data_dir / "Validation"),
    transform=transform
)

train_loader = DataLoader(
    train_dataset,
    batch_size=32,
    shuffle=True,
    num_workers=0
)

val_loader = DataLoader(
    val_dataset,
    batch_size=32,
    shuffle=False,
    num_workers=0
)

print("Class mapping:", train_dataset.class_to_idx)
print("Training images:", len(train_dataset))
print("Validation images:", len(val_dataset))

images, labels = next(iter(train_loader))
print("Image batch shape:", images.shape)
print("Label batch shape:", labels.shape)
```

### Expected Output

The counts and class mapping should correspond to the files actually present in the repository. For the reported dataset, the expected counts are:

```text
Training images: 1181
Validation images: 410
```

The class mapping is determined alphabetically by `ImageFolder`, rather than by a manually assigned label order.

**Note:** `ImageFolder` requires class-specific subdirectories. The example therefore loads Training and Validation only; the Testing directory requires appropriate labels and directory organization or a custom dataset loader.

## Suggested Research Workflow

1. **Dataset verification:** Check image integrity, labels, class distribution, and duplicate images.
2. **Data preparation:** Select suitable image resizing, normalization, and preprocessing techniques.
3. **Training:** Train an appropriate CNN or transfer-learning model using the Training subset.
4. **Validation:** Tune hyperparameters and select the model using the Validation subset.
5. **Testing:** Evaluate the selected model on a separate, appropriately labeled held-out test set.
6. **Performance analysis:** Report accuracy, precision, recall, F1-score, confusion matrix, and ROC-AUC where appropriate.
7. **Explainability:** Investigate model predictions using Grad-CAM or related methods.
8. **Reproducibility:** Document random seeds, software versions, preprocessing, hyperparameters, and experimental settings.

## Important Considerations

- **Prevent data leakage:** Keep the testing subset separate from training and model selection.
- **Verify sample independence:** Where possible, partition images from the same physical powder sample or acquisition session into the same subset.
- **Document labeling:** Clearly explain the experimental or annotation protocol used to assign the Mixed and Not Mixed labels.
- **Report class distributions:** Include verified counts for every subset.
- **Avoid unsupported claims:** High classification performance does not independently validate pharmaceutical content uniformity.
- **Respect data rights:** Ensure that the images may legally be shared and reused under the selected license.

## Citation

If you use this dataset in research, please acknowledge the repository:

Patel, A. *Drug Powder Uniformity Dataset*. GitHub repository. Available at:

https://github.com/abhicse8379/drug-powder-uniformity-dataset

If a formal publication or DOI becomes available, update this citation to include the associated bibliographic information.

## License

Refer to the [`LICENSE`](https://github.com/abhicse8379/drug-powder-uniformity-dataset/blob/main/LICENSE) file for the applicable terms of use.

Before redistributing the dataset, confirm that the license is present in the repository and that you have permission to license all included images.

## Disclaimer

This dataset is provided for research and educational purposes. It has not, by itself, been established as a validated pharmaceutical quality-control method. Research findings based on these images should not replace appropriate laboratory testing, established analytical methods, or applicable regulatory requirements.

## Contact

For questions, dataset feedback, or research collaboration, please contact the repository maintainer through GitHub:

**Abhishek Patel**  
GitHub: [@abhicse8379](https://github.com/abhicse8379)

---

If you use this dataset, please cite the repository and describe its use transparently in your research publication.
