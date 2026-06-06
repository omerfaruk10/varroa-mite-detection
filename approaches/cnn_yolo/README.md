\# CNN and YOLO Experiments



This folder contains the CNN-based classification and YOLO-based object detection experiments conducted for Varroa mite detection.



All preprocessing, training, validation, external validation, result table creation, and graph generation steps were performed in a single Google Colab notebook.



\## Notebook



The main notebook is located in:



```text

notebooks/cnn\_yolo\_all\_experiments.ipynb

```



This notebook includes:



\* Dataset download and preparation

\* YOLO label preprocessing

\* Binary classification dataset creation

\* ResNet18 training and evaluation

\* EfficientNet-B0 training and evaluation

\* YOLOv8n training and evaluation

\* YOLO26n training and evaluation

\* Internal validation

\* External validation

\* Result table creation

\* Performance graph generation



\## Models



The following models were trained and evaluated in this section.



\### CNN-based Classification Models



\* ResNet18

\* EfficientNet-B0



These models were used for binary image classification. The classification task includes two classes:



```text

varroa

no\_varroa

```



\### YOLO-based Object Detection Models



\* YOLOv8n

\* YOLO26n



These models were used for object detection. Unlike classification models, YOLO-based models detect the location of Varroa mites in the image using bounding boxes.



\## Datasets



The experiments used three datasets:



\* Varroa Dataset

\* HoneyBee VarroaMite

\* Varroa Mites Detector



Varroa Dataset and HoneyBee VarroaMite were used for model training and internal validation.



Varroa Mites Detector was used as an external validation dataset. This dataset was not used during model training. It was used to evaluate how well the trained models generalize to a different data source.



\## Preprocessing



For YOLO-based object detection models, the datasets were converted into a single-class detection format:



```text

0: varroa

```



Invalid bounding boxes were removed during preprocessing. Empty label files were preserved as negative/background examples.



For CNN-based classification models, YOLO annotation files were converted into a binary classification structure. Images containing at least one valid Varroa bounding box were labeled as `varroa`. Images without a valid Varroa label were labeled as `no\_varroa`.



\## Input Sizes



| Model           | Input Size |

| --------------- | ---------- |

| ResNet18        | 224x224    |

| EfficientNet-B0 | 224x224    |

| YOLOv8n         | 640x640    |

| YOLO26n         | 640x640    |



\## Evaluation Metrics



Classification models were evaluated using:



\* Accuracy

\* Precision

\* Recall

\* F1-score



YOLO-based object detection models were evaluated using:



\* Precision

\* Recall

\* F1-score

\* mAP50

\* mAP50-95



\## Outputs



Generated graphs and result visualizations are stored in:



```text

outputs/

```



The output folder includes:



\* `classification\_external\_accuracy.png`

\* `classification\_f1\_comparison.png`

\* `classification\_recall\_comparison.png`

\* `yolo\_f1\_comparison.png`

\* `yolo\_map50\_comparison.png`

\* `yolo\_map50\_95\_comparison.png`

\* `yolo\_recall\_comparison.png`



\## Results Summary



Among the CNN-based classification models, EfficientNet-B0 trained on the Varroa Dataset achieved the strongest external validation result.



Among the YOLO-based object detection models, YOLOv8n trained on the Varroa Dataset achieved the strongest external validation result.



The results showed that models trained on the Varroa Dataset generally achieved better external validation performance than models trained on the HoneyBee VarroaMite dataset. This indicates that dataset distribution and annotation consistency have an important effect on model generalization.



\## Folder Structure



```text

cnn\_yolo/

│

├── notebooks/

│   └── cnn\_yolo\_all\_experiments.ipynb

│

├── outputs/

│   ├── classification\_external\_accuracy.png

│   ├── classification\_f1\_comparison.png

│   ├── classification\_recall\_comparison.png

│   ├── yolo\_f1\_comparison.png

│   ├── yolo\_map50\_comparison.png

│   ├── yolo\_map50\_95\_comparison.png

│   └── yolo\_recall\_comparison.png

│

└── README.md

```



\## Notes



Large datasets and trained model weight files are not included in this repository.



The datasets were downloaded and processed in Google Colab during the experimental process. Model weight files such as `best.pt` and `last.pt` were excluded because of file size limitations.



Roboflow API keys and personal Google Drive paths should not be committed to the repository.



