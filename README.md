# Drug Powder Uniformity Dataset

**A Microscopic Image Dataset for Deep Learning-Based Pharmaceutical Powder Mixing Uniformity Classification**

[![Task](https://img.shields.io/badge/Task-Binary%20Classification-blue)](https://github.com/abhicse8379/drug-powder-uniformity-dataset)
[![Framework](https://img.shields.io/badge/Framework-PyTorch-red)](https://pytorch.org/)
[![Images](https://img.shields.io/badge/Images-1%2C731-green)](https://github.com/abhicse8379/drug-powder-uniformity-dataset)

## 1. Overview

The **Drug Powder Uniformity Dataset** is a microscopic image dataset developed to support research on automated pharmaceutical powder mixing uniformity assessment using computer vision and deep learning.

The dataset is designed for binary image classification, distinguishing between powder samples labeled as **Mixed** and **Not Mixed**. It can be used to investigate convolutional neural networks (CNNs), transfer learning, image preprocessing, data augmentation, model generalization, and explainable artificial intelligence (XAI).

Automated microscopic image analysis may provide a complementary approach for studying powder mixing characteristics and developing computer vision-assisted pharmaceutical process monitoring systems.

## 2. Dataset Information

| Attribute | Description |
|---|---|
| Dataset Name | Drug Powder Uniformity Dataset |
| Data Type | Microscopic images |
| Application Domain | Pharmaceutical powder mixing |
| Machine Learning Task | Binary image classification |
| Number of Classes | 2 |
| Total Images | 1,731 |
| Training Images | 1,181 |
| Validation Images | 410 |
| Testing Images | 140 |
| Deep Learning Framework | PyTorch |
| Repository | GitHub |

## 3. Classification Categories

### Mixed (Class 0)

Images labeled as Mixed represent powder samples classified as adequately mixed according to the dataset's labeling protocol.

### Not Mixed (Class 1)

Images labeled as Not Mixed represent powder samples classified as inadequately mixed or non-uniform according to the dataset's labeling protocol.

### Label Mapping

| TARGET | Class Label |
|---:|---|
| 0 | Mixed |
| 1 | Not Mixed |

The numerical labels above apply to the provided testing-image annotations. PyTorch's `ImageFolder` assigns class indices alphabetically, so its automatically generated class mapping may differ from the TARGET mapping.

## 4. Dataset Structure

The dataset is organized into three subsets: Training, Validation, and Testing.

```text
drug-powder-uniformity-dataset/
├── Testing/
│   ├── 20211129_120203.jpg
│   ├── 20210924_134441.jpg
│   └── ... (140 images)
│
├── Training/
│   ├── Mixed/
│   │   └── ... (548 images)
│   └── Not Mixed/
│       └── ... (633 images)
│
└── Validation/
    ├── Mixed/
    │   └── ... (192 images)
    └── Not Mixed/
        └── ... (218 images)
```

**Note:** The Testing directory contains image files, with their ground-truth labels represented by the supplied testing-image annotation table. The table includes the image identifier, image filename, and TARGET label.

## 5. Dataset Statistics

The dataset contains **1,731 microscopic images** across the three subsets.

| Dataset Split | Mixed (Class 0) | Not Mixed (Class 1) | Total |
|---|---:|---:|---:|
| Training | 548 | 633 | 1,181 |
| Validation | 192 | 218 | 410 |
| Testing | 119 | 21 | 140 |
| **Total** | **859** | **872** | **1,731** |

*The testing class counts are based on the provided 140-row annotation list and should be cross-checked against the original annotation file before publication.*

### Dataset Distribution

- **Training:** 1,181 images
- **Validation:** 410 images
- **Testing:** 140 images

The Training and Validation subsets contain separate Mixed and Not Mixed folders. The Testing subset is accompanied by image-level annotations for evaluation.

## 6. Intended Applications

The dataset may be used for:

- Microscopic pharmaceutical powder image classification
- Deep learning-based powder mixing assessment
- CNN architecture comparison and transfer learning
- Image preprocessing and data augmentation experiments
- Feature extraction and representation learning
- Model generalization and robustness analysis
- Explainable AI using Grad-CAM and related methods
- Research into computer vision-assisted pharmaceutical process monitoring

## 7. Getting Started

### Clone the Repository

```bash
git clone https://github.com/abhicse8379/drug-powder-uniformity-dataset.git
cd drug-powder-uniformity-dataset
```

### Install Dependencies

Install the Python libraries required for the example:

```bash
pip install torch torchvision matplotlib scikit-learn pillow pandas
```

For GPU-based experiments, install a PyTorch version compatible with your operating system and CUDA environment using the official [PyTorch installation guide](https://pytorch.org/get-started/locally/).

## 8. Loading Training and Validation Data with PyTorch

The following example loads the class-organized Training and Validation subsets using `torchvision.datasets.ImageFolder`.

```python
from pathlib import Path
from torchvision import datasets, transforms
from torch.utils.data import DataLoader

DATA_DIR = Path(".")

transform = transforms.Compose([
    transforms.Resize((224, 224)),
    transforms.ToTensor()
])

train_dataset = datasets.ImageFolder(
    root=str(DATA_DIR / "Training"),
    transform=transform
)

val_dataset = datasets.ImageFolder(
    root=str(DATA_DIR / "Validation"),
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

Expected image counts:

```text
Training images: 1181
Validation images: 410
```

**Important:** `ImageFolder` assigns class indices according to alphabetical folder order. If you need the exact mapping `Mixed = 0` and `Not Mixed = 1`, explicitly verify the mapping or define it in your training pipeline.

The example resizes images to 224 × 224 pixels. This is a configurable preprocessing choice, not a claim about the original image dimensions.

## 9. Evaluating the Testing Set

The Testing subset contains 140 images with corresponding ground-truth TARGET annotations.

| TARGET | Class | Reported Images |
|---:|---|---:|
| 0 | Mixed | 119 |
| 1 | Not Mixed | 21 |
| **Total** | | **140** |

The testing images can be evaluated using a custom PyTorch dataset that reads filenames and labels from a CSV annotation file.

A suitable annotation file can use the following columns:

```csv
ID,Image_Name,TARGET
20211129_120203,20211129_120203.jpg,0
20210924_134441,20210924_134441.jpg,0
20211018_160742,20211018_160742.jpg,1
```

This is an illustrative excerpt. Use the complete annotation table for actual evaluation.

The model should be evaluated on the held-out testing set only after the model architecture, preprocessing, and hyperparameters have been selected using the Training and Validation subsets.

## 10. Suggested Research Workflow

1. **Dataset verification:** Validate filenames, image integrity, labels, and class distributions.
2. **Preprocessing:** Select suitable image resizing, normalization, and preprocessing techniques.
3. **Model training:** Train CNN-based or transfer-learning models using the Training subset.
4. **Model selection:** Use the Validation subset for hyperparameter tuning and model selection.
5. **Final evaluation:** Evaluate the selected model on the held-out Testing subset.
6. **Performance analysis:** Report accuracy, precision, recall, F1-score, confusion matrix, and ROC-AUC where appropriate.
7. **Explainability:** Use Grad-CAM or related methods to investigate model predictions.
8. **Reproducibility:** Document random seeds, software versions, model architecture, and experimental settings.

## 11. Important Research Considerations

- **Prevent data leakage:** Keep the Testing subset separate from training and model selection.
- **Check sample independence:** Images from the same physical sample or acquisition session should be assigned appropriately to avoid overly optimistic evaluation.
- **Document ground truth:** Clearly describe the experimental or annotation protocol used to determine mixing labels.
- **Consider class imbalance:** The Testing subset contains fewer Not Mixed images than Mixed images, so report class-wise metrics in addition to overall accuracy.
- **Use appropriate validation:** Ensure that image augmentation is applied only to training data, unless a different evaluation protocol is explicitly justified.
- **Avoid unsupported conclusions:** Classification performance alone does not establish pharmaceutical content uniformity or regulatory compliance.

## 12. Citation

If you use this dataset in research, please acknowledge the repository:

Patel, A. *Drug Powder Uniformity Dataset*. GitHub repository.

https://github.com/abhicse8379/drug-powder-uniformity-dataset

If a formal publication or DOI becomes available, update this citation with the associated bibliographic information.

## 13. License

No license has been specified for this dataset at present. Unless and until a license is added, all rights remain with the copyright holder. Please contact the repository owner for permission before redistributing, modifying, or using the dataset beyond what is permitted by applicable law.

## 14. Disclaimer

This dataset is intended for research and educational purposes. It is not, by itself, a validated pharmaceutical quality-control method. Findings obtained from these images should not replace appropriate laboratory testing, established analytical methods, or applicable regulatory requirements.

## 15. Contact

**Abhishek Patel**

GitHub: [@abhicse8379](https://github.com/abhicse8379)

For questions, dataset feedback, or research collaboration, please contact the repository maintainer through GitHub.

---

If you use this dataset, please cite the repository and transparently describe its use, preprocessing, and evaluation protocol in your research publication.
