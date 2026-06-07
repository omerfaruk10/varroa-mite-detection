# Traditional ML

This folder contains the traditional machine learning workflow used for Varroa mite classification and detection.

The approach is based on patch-level feature extraction, classical classification models, and sliding-window detection with trained patch classifiers.

## Scope

In this approach, three classical machine learning models were studied:

* **Linear SVM**
* **RBF SVM**
* **Random Forest**

The classification models were trained to classify image patches as:

* `varroa`
* `no_varroa`

After patch-level classification, the selected models were also evaluated in an object detection setting. Detection was performed by scanning images with sliding windows and converting high-confidence patch predictions into bounding box candidates.

---

## Folder Structure

```bash
traditional_ml/
|-- inputs/
|   |-- 06_selected_model_training/
|   |-- 07_classification_final_test/
|   |-- 08_detection_screening/
|   |-- 09_detection_tuning/
|   |-- 10_final_internal_test/
|   `-- 11_external_validation/
|-- notebooks/
|   |-- 00_project_setup/
|   |-- 01_exploration/
|   |-- 02_patch_preparation/
|   |-- 03_feature_engineering/
|   |-- 04_linear_svm_model_training/
|   |-- 05_linear_svm_classification_validation/
|   |-- 06_selected_model_training/
|   |-- 07_classification_final_test/
|   |-- 08_detection_screening/
|   |-- 09_detection_tuning/
|   |-- 10_final_internal_test/
|   `-- 11_external_validation/
|-- outputs/
|   |-- 00_project_setup/
|   |-- 01_exploration/
|   |-- 02_patch_preparation/
|   |-- 03_feature_engineering/
|   |-- 04_linear_svm_model_training/
|   |-- 05_linear_svm_classification_validation/
|   |-- 06_selected_model_training/
|   |-- 07_classification_final_test/
|   |-- 08_detection_screening/
|   |-- 09_detection_tuning/
|   |-- 10_final_internal_test/
|   `-- 11_external_validation/
`-- README.md
```

---

## Inputs

The `inputs/` folder contains small stage-level CSV files that are needed by later notebooks. These files are used as fixed handoff inputs between stages.

Examples include:

* selected candidate model tables
* selected validation image subsets
* finalized detection parameter tables
* external validation finalist model lists

Raw datasets, extracted feature files, PCA artifacts, and trained model files are not stored in `inputs/`.

---

## Pipeline Stages

### 00. Project Setup

Checks the project folder structure and verifies that the required data directories are available.

### 01. Dataset Exploration

Explores the datasets by checking image files, YOLO label files, image-label matching, image sizes, and object count distributions.

### 02. Patch Preparation

Creates positive and negative image patches from the annotated datasets. These patches are used for patch-level binary classification.

### 03. Feature Engineering

Extracts handcrafted features from image patches.

The extracted feature groups include:

* HOG features
* HSV color histogram features
* LBP texture features
* PCA-reduced HOG features
* combined feature sets

Feature files are stored under the project-level `data/features/` directory.

### 04. Linear SVM Model Training

Trains Linear SVM models using different patch sets and feature combinations.

### 05. Linear SVM Classification Validation

Evaluates Linear SVM candidates on validation data and selects promising model-feature combinations for the next stage.

### 06. Selected Model Training

Trains selected RBF SVM and Random Forest models using the candidate combinations selected from the previous validation stage.

### 07. Classification Final Test

Evaluates selected classification models on the final internal test split.

### 08. Detection Screening

Performs preliminary detection experiments to screen detection-related parameters such as threshold, stride, and post-processing behavior.

### 09. Detection Tuning

Tunes detection parameters on validation images using selected classification models.

### 10. Final Internal Test

Evaluates the final selected detection configuration on the internal test set.

### 11. External Validation

Evaluates the final traditional machine learning models on the external validation dataset.

---

## Datasets

Three datasets were used in this approach:

1. **Varroa Dataset**
2. **HoneyBee VarroaMite**
3. **Varroa Mites Detector**

### Dataset Usage

* **Varroa Dataset** was used for training, internal validation, and internal testing.
* **HoneyBee VarroaMite** was used for training, internal validation, and internal testing.
* **Varroa Mites Detector** was used as the external validation dataset.

The external validation dataset was not used during model training. It was used to evaluate generalization on a different data source.

---

## Feature Engineering

Traditional machine learning models require fixed-length feature vectors. For this reason, image patches were converted into handcrafted feature representations.

The main feature extraction methods were:

| Feature Type | Description |
| ------------ | ----------- |
| HOG | Captures local gradient and shape patterns |
| HSV Histogram | Captures color distribution information |
| LBP | Captures local texture patterns |
| PCA-HOG | Reduces high-dimensional HOG features |
| Combined Features | Combines multiple feature groups |

---

## Models

### Classification Models

| Model | Task | Output |
| ----- | ---- | ------ |
| Linear SVM | Patch classification | `varroa` / `no_varroa` |
| RBF SVM | Patch classification | `varroa` / `no_varroa` |
| Random Forest | Patch classification | `varroa` / `no_varroa` |

### Detection Method

| Method | Description |
| ------ | ----------- |
| Sliding-window detection | Scans images using patch windows and classifies each candidate region |
| Post-processing | Merges or filters candidate boxes based on detection parameters |

---

## Evaluation Metrics

### Classification Metrics

The classification models were evaluated using:

* Accuracy
* Precision
* Recall
* F1-score
* Balanced accuracy
* Confusion matrix

### Detection Metrics

The detection experiments were evaluated using:

* Precision
* Recall
* F1-score
* IoU-based matching
* Per-image detection summaries

---

## Model And Feature Artifacts

The notebooks reference larger artifacts from project-level folders:

```text
data/features/
outputs/models/
```

These artifacts include extracted feature parquet files, PCA objects, and trained model files. They are not duplicated inside `approaches/traditional_ml/`.

---

## Outputs

Generated tables and figures are stored in the `outputs/` folder.

The output folders follow the same stage structure as the notebooks. Most output folders contain:

* `tables/`: CSV files with summaries, metrics, rankings, and evaluation details
* `figures/`: PNG files with plots and visual checks, when relevant

Large trained model files and large feature files are not stored in this folder.

---

## Notes

Experiments were conducted in local Python and notebook environments.

Large datasets, extracted feature parquet files, PCA artifacts, and trained model files are expected under the project-level `data/` and `outputs/models/` directories.

Notebook execution outputs are cleared before committing the notebooks.
