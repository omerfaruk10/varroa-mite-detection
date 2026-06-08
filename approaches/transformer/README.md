

# Transformers for Object Detection

This folder contains the Vision Transformer-based object detection experiments conducted for the Varroa mite detection project.

## Scope

In this approach, three state-of-the-art Transformer-based object detection models were studied:

* **DETR (DEtection TRansformer)**
* **Deformable DETR**
* **RT-DETR (Real-Time DEtection TRansformer)**

Unlike the baseline binary classification models, these models focus on multi-class and single-class localization. The dataset is configured to detect and differentiate:

* `bee`
* `varroa`

The primary objective is to evaluate the self-attention mechanism's capability in detecting tiny objects (Varroa mites) on honeybees compared to traditional CNN and anchor-based architectures.

---

## Folder Structure

```bash
transformers_detection/
├── notebooks/
│   ├── DETR_DEFORMABLE_DETR_EĞİTİMLERİ_1.ipynb
│   ├── DETR_DEFORMABLE_DETR_EĞİTİMLERİ_2.ipynb
│   └── RT-DETR_EĞİTİMLERİ.ipynb
├── outputs/
│   ├── transformer_f1_comparison.png
│   ├── transformer_map50_95_comparison.png
│   ├── transformer_map50_comparison.png
│   ├── transformer_precision_comparison.png
│   └── transformer_recall_comparison.png
└── README.md

```

---

## Notebooks

### 1. `DETR_DEFORMABLE_DETR_EĞİTİMLERİ_1.ipynb` & `DETR_DEFORMABLE_DETR_EĞİTİMLERİ_2.ipynb`

These notebooks implement the training and evaluation pipelines for vanilla **DETR** and **Deformable DETR** using the Hugging Face `transformers` library.

Key processes include:

* Fetching datasets via the Roboflow API using the **COCO JSON** annotation standard.
* Resolving class alignment and label mapping mismatches (`id2label`) to handle both `bee` and `varroa` categories properly.
* Implementing target image processors (`DeformableDetrImageProcessor`) optimized for attention-mask generations.
* Managing persistent checkpoints by saving intermediate weights directly to Google Drive during long training sequences.

### 2. `RT-DETR_EĞİTİMLERİ.ipynb`

This notebook explores the real-time capabilities of end-to-end object detection transformers using **RT-DETR** via the `ultralytics` framework.

Key processes include:

* Preparing datasets in the strict YOLO/Ultralytics text format.
* Training models with multi-scale feature extractors tailored for high frame-rate performance without sacrificing the transformer encoder's spatial awareness.

---

## Evaluation Metrics

The performance of the Transformer models was benchmarked using standard computer vision object detection metrics:

* **Precision**
* **Recall**
* **F1-score**
* **mAP50** (Mean Average Precision at an Intersection over Union threshold of 0.50)
* **mAP50-95** (Mean Average Precision averaged over ten IoU thresholds from 0.50 to 0.95)

---

## Outputs

The comparative visualization charts across all evaluated transformer architectures are stored in the `outputs/` directory:

* `transformer_precision_comparison.png` — Evaluates exact bounding-box verification constraints.
* `transformer_recall_comparison.png` — Measures the model's capacity to minimize missed Varroa detections.
* `transformer_f1_comparison.png` — Highlights the harmonic balance between Precision and Recall.
* `transformer_map50_comparison.png` — Standard validation at 0.50 IoU.
* `transformer_map50_95_comparison.png` — Strict multi-threshold localization matrix.

---

## Results Summary

* **RT-DETR (Real-Time DEtection TRansformer):** Demonstrated exceptional performance across all benchmarks, achieving the highest **mAP50-95 (~0.58)**, **mAP50 (~0.85)**, and an **F1-score above 0.80**. It establishes itself as the superior backbone for edge or real-time deployment fields in this project.
* **Deformable DETR:** Successfully resolved the slow convergence limitations of vanilla transformer architectures. It showed stable localization metrics (**mAP50 ~0.65**) and proved highly effective at extracting multi-scale features for complex overlapping targets.
* **DETR:** While displaying fair baseline properties (**mAP50 ~0.46**), it lagged behind newer architectures in processing constraints and fine-grained localization matrix distributions.

---

## Notes

* All computational sessions were processed inside **Google Colab** using high-performance hardware environments running **NVIDIA A100 GPUs**.
* Massive dataset caches, raw weight outputs (`.pt` files, config `.json` dumps), and heavy Hugging Face hubs are structurally excluded via `.gitignore`.
* Private infrastructure tokens, including personal Roboflow Private API keys or mounted cloud paths, must not be pushed to public commits.
