# AI-Based Varroa Mite Detection in Honey Bee Colonies

Comparative AI-based computer vision project for Varroa mite classification and detection in honey bee images using traditional machine learning, CNN/YOLO, and Transformer-based object detection models.

## Overview

Varroa destructor is one of the major biological threats to honey bee colonies. Manual inspection methods such as visual counting, powdered sugar tests, alcohol washing, and sticky board monitoring can be time-consuming, error-prone, and sometimes harmful to bees.

This project investigates image processing and artificial intelligence-based methods for detecting Varroa mites in honey bee images. The work evaluates the problem from two perspectives:

- Binary classification: deciding whether an image or image patch contains Varroa.
- Object detection: locating Varroa mites with bounding boxes.

The project compares three model families under internal and external validation settings to analyze both performance and generalization.

## Approaches

| Approach | Models | Main Task |
| --- | --- | --- |
| Traditional ML | Linear SVM, RBF SVM, Random Forest | Patch-level classification and sliding-window detection |
| CNN and YOLO | ResNet18, EfficientNet-B0, YOLOv8n, YOLOv26n | Image classification and bounding-box detection |
| Transformers | DETR, Deformable DETR, RT-DETR | Small object detection |

### Traditional Machine Learning

The traditional ML pipeline uses handcrafted visual features extracted from positive and negative image patches:

- HOG features
- HSV color histograms
- LBP texture features
- PCA-reduced HOG features
- Combined feature sets

SVM and Random Forest models are trained for binary Varroa/no-Varroa classification. Selected classifiers are also used in a sliding-window detection pipeline to generate candidate bounding boxes on full images.

See [approaches/traditional_ml](approaches/traditional_ml/README.md).

### CNN and YOLO

The CNN/YOLO workflow contains two task-specific pipelines:

- ResNet18 and EfficientNet-B0 for binary image classification.
- YOLOv8n and YOLOv26n for single-class Varroa object detection.

YOLO annotations are converted into a single-class `varroa` format, and empty label files are preserved as negative/background samples.

See [approaches/cnn_yolo](approaches/cnn_yolo/README.md).

### Transformer-Based Detection

Transformer-based detection experiments evaluate attention-based object detectors for small object localization:

- DETR
- Deformable DETR
- RT-DETR

These models are used to compare the effect of global attention, multi-scale representation, and anchor-free detection on tiny Varroa mite localization.

See [approaches/transformer](approaches/transformer/README.md).

## Datasets

Three datasets are used in the experimental workflow:

1. Varroa Dataset
2. HoneyBee VarroaMite
3. Varroa Mites Detector

The first two datasets are used for development, training, internal validation, and internal testing depending on the experiment. The Varroa Mites Detector dataset is used as an independent external validation dataset and is not used during model training.

Large datasets, extracted feature files, trained model weights, and generated artifacts are not committed to this repository.

## Evaluation

The project evaluates model performance with task-specific metrics:

Classification metrics:

- Accuracy
- Precision
- Recall
- F1-score
- Balanced accuracy
- Confusion matrix

Object detection metrics:

- Precision
- Recall
- F1-score
- IoU-based matching
- mAP50
- mAP50-95

Both internal validation and independent external validation are used to measure generalization across different data distributions, image characteristics, and annotation quality.

## Results Summary

Key findings from the comparative experiments:

- Traditional ML models, especially SVM-based approaches, achieved strong external classification performance.
- EfficientNet-B0 provided a balanced CNN-based classification baseline.
- YOLO models produced strong internal detection results but were more sensitive to dataset distribution shifts.
- Transformer-based models, especially RT-DETR, achieved the strongest external object detection performance.
- External validation showed that dataset selection, image quality, annotation consistency, and the small size of the target object strongly affect real-world performance.

## Repository Structure

```text
.
|-- approaches/
|   |-- traditional_ml/
|   |-- cnn_yolo/
|   `-- transformer/
|-- data/
|   `-- README.md
|-- docs/
|   |-- presentation/
|   `-- reports/
|-- requirements/
|   |-- traditional_ml.txt
|   |-- cnn_yolo.txt
|   `-- transformer.txt
|-- .gitignore
`-- README.md
```

## Setup

Create a Python environment and install the dependencies for the workflow you want to run.

Traditional ML:

```bash
pip install -r requirements/traditional_ml.txt
```

CNN and YOLO:

```bash
pip install -r requirements/cnn_yolo.txt
```

Transformer experiments:

```bash
pip install -r requirements/transformer.txt
```

## Project Documents

The final project report and presentation are available under:

- [docs/reports](docs/reports)
- [docs/presentation](docs/presentation)

