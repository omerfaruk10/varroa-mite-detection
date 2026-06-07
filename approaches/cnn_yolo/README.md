# CNN and YOLO

This folder contains the CNN-based classification and YOLO-based object detection experiments conducted for the Varroa mite detection project.

## Scope

In this approach, four deep learning models were studied:

* **ResNet18**
* **EfficientNet-B0**
* **YOLOv8n**
* **YOLO26n**

The classification models, **ResNet18** and **EfficientNet-B0**, were used for binary image classification. The goal of these models is to classify each image as:

* `varroa`
* `no_varroa`

The object detection models, **YOLOv8n** and **YOLO26n**, were used for single-class Varroa mite detection. These models aim to detect the location of Varroa mites in images using bounding boxes.

---

## Folder Structure

```bash
cnn_yolo/
├── notebooks/
│   ├── cnn_classification_resnet_efficientnet.ipynb
│   └── yolo_detection_yolov8_yolo26.ipynb
├── outputs/
│   ├── classification_external_accuracy.png
│   ├── classification_f1_comparison.png
│   ├── classification_recall_comparison.png
│   ├── yolo_f1_comparison.png
│   ├── yolo_map50_comparison.png
│   ├── yolo_map50_95_comparison.png
│   └── yolo_recall_comparison.png
└── README.md
```

---

## Notebooks

### 1. `cnn_classification_resnet_efficientnet.ipynb`

This notebook contains the CNN-based binary classification experiments.

It includes:

* dataset download and preparation
* YOLO label reading
* binary classification dataset creation
* `varroa` / `no_varroa` label generation
* ResNet18 training and evaluation
* EfficientNet-B0 training and evaluation
* internal validation
* external validation
* classification metric comparison
* classification graph generation

### 2. `yolo_detection_yolov8_yolo26.ipynb`

This notebook contains the YOLO-based object detection experiments.

It includes:

* dataset download and preparation
* YOLO label preprocessing
* conversion to single-class `varroa` detection format
* invalid bounding box cleaning
* YOLOv8n training and evaluation
* YOLO26n training and evaluation
* internal validation
* external validation
* detection metric comparison
* YOLO graph generation

---

## Datasets

Three datasets were used in this approach:

1. **Varroa Dataset**
2. **HoneyBee VarroaMite**
3. **Varroa Mites Detector**

### Dataset Usage

* **Varroa Dataset** was used for training and internal validation.
* **HoneyBee VarroaMite** was used for training and internal validation.
* **Varroa Mites Detector** was used as the external validation dataset.

The external validation dataset was not used during model training. It was used to evaluate how well the trained models generalize to a different data source.

---

## Preprocessing

For YOLO-based object detection models, all valid Varroa labels were converted into a single-class detection format:

```text
0: varroa
```

Invalid bounding boxes were removed during preprocessing. Empty label files were preserved as negative/background samples.

For CNN-based classification models, YOLO annotation files were converted into a binary classification structure. Images containing at least one valid Varroa bounding box were labeled as `varroa`. Images without a valid Varroa label were labeled as `no_varroa`.

---

## Models

### Classification Models

| Model           | Task                  | Output                 |
| --------------- | --------------------- | ---------------------- |
| ResNet18        | Binary classification | `varroa` / `no_varroa` |
| EfficientNet-B0 | Binary classification | `varroa` / `no_varroa` |

### Object Detection Models

| Model   | Task             | Output         |
| ------- | ---------------- | -------------- |
| YOLOv8n | Object detection | Bounding boxes |
| YOLO26n | Object detection | Bounding boxes |

---

## Input Sizes

| Model           | Input Size |
| --------------- | ---------- |
| ResNet18        | 224x224    |
| EfficientNet-B0 | 224x224    |
| YOLOv8n         | 640x640    |
| YOLO26n         | 640x640    |

---

## Evaluation Metrics

### Classification Metrics

The classification models were evaluated using:

* Accuracy
* Precision
* Recall
* F1-score

### Object Detection Metrics

The YOLO-based object detection models were evaluated using:

* Precision
* Recall
* F1-score
* mAP50
* mAP50-95

---

## Outputs

Generated result graphs are stored in the `outputs/` folder.

### Classification Graphs

* `classification_external_accuracy.png`
* `classification_f1_comparison.png`
* `classification_recall_comparison.png`

### YOLO Graphs

* `yolo_f1_comparison.png`
* `yolo_map50_comparison.png`
* `yolo_map50_95_comparison.png`
* `yolo_recall_comparison.png`

---

## Results Summary

Among the CNN-based classification models, **EfficientNet-B0 trained on the Varroa Dataset** achieved the strongest external validation result.

Among the YOLO-based object detection models, **YOLOv8n trained on the Varroa Dataset** achieved the strongest external validation result.

The results showed that models trained on the Varroa Dataset generally achieved better external validation performance than models trained on the HoneyBee VarroaMite dataset. This indicates that dataset distribution, image characteristics, and annotation consistency have an important effect on model generalization.

---

## Notes

Experiments were mainly conducted in **Google Colab**.

Large datasets and trained model weight files are not included in this repository. Model weight files such as `best.pt` and `last.pt` were excluded because of file size limitations.

Roboflow API keys and personal Google Drive paths should not be committed to the repository.
