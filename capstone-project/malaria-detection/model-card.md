# Model Card: Faster R-CNN ResNet50 FPN Models for Malaria Cell Detection and Classification
## Author
Harjinder Chandi, Junept Limited

## Model Details
This document compares four object detection models based on Faster R-CNN with a ResNet-50 backbone and Feature Pyramid Network (FPN), trained for malaria cell detection and classification. The models differ in FPN version (v1 or v2) and loss function (Weighted Cross-Entropy or Weighted Focal Loss). These models detect and classify malaria cell types in microscopic blood smear images using a Faster R-CNN architecture with a ResNet-50 FPN V1 or V2 backbone. These are trained on the P. vivax malaria dataset from Kaggle, leveraging annotated bounding boxes and cell categories. These models address severe class imbalance using weighted loss functions and oversampling strategies, aiming for robust detection of both common and rare cell types.

## Model Comparison Tables

### Models
| Model Name                                      | FPN Version | Loss Function           |
|-------------------------------------------------|-------------|-------------------------|
| faster-rcnn-resnet50-fpn-weighted-CE-loss       | v1          | Weighted Cross-Entropy  |
| faster-rcnn-resnet50-fpn-weighted-focal-loss    | v1          | Weighted Focal Loss     |
| faster-rcnn-resnet50-fpn-v2-weighted-CE-loss    | v2          | Weighted Cross-Entropy  |
| faster-rcnn-resnet50-fpn-v2-weighted-focal-loss | v2          | Weighted Focal Loss     |

### Training Details
| Model Name                                      | Pretrained Weights | Loss Weighting                | Optimizer           |
|-------------------------------------------------|--------------------|-----------------------------------------------------|---------------------|
| faster-rcnn-resnet50-fpn-weighted-CE-loss       | COCO               | Cross-Entropy loss + Class weights (inverse freq.)  | SGD with momentum   |
| faster-rcnn-resnet50-fpn-weighted-focal-loss    | COCO               | Focal loss + class weights (inverse freq.)          | SGD with momentum   |
| faster-rcnn-resnet50-fpn-v2-weighted-CE-loss    | COCO               | Cross-Entropy loss + Class weights (inverse freq.)  | SGD with momentum   |
| faster-rcnn-resnet50-fpn-v2-weighted-focal-loss | COCO               | Focal loss + class weights (inverse freq.)          | SGD with momentum   |

### Model Differences and Comparison
| Feature                | v1 Models                                   | v2 Models                                   |
|------------------------|---------------------------------------------|---------------------------------------------|
| FPN Version            | Original FPN                                | Improved FPN (better normalization, weights)|
| Preprocessing/Weights  | Standard                                    | Improved                                    |
| Expected Accuracy      | Good                                        | Better                                      |

| Feature                | Weighted CE Loss Models                     | Weighted Focal Loss Models                  |
|------------------------|---------------------------------------------|---------------------------------------------|
| Loss Function          | Weighted Cross-Entropy                      | Weighted Focal Loss                         |
| Class Imbalance        | Good for moderate imbalance                 | Better for severe imbalance                 |
| Hyperparameter Tuning  | Simpler                                     | Focal loss params may need tuning           |

## Model Specifications
### Model Type
- Object Detection (Bounding Box + Classification)

### Model Architecture
- Purpose: Object detection and classification of malaria cell types in blood smear images
- Backbone: Faster R-CNN with ResNet-50 backbone and Feature Pyramid Network FPN v1 or FPN v2
- Detection Head: Faster R-CNN with either Weighted Cross-Entropy Loss or Weighted Focal Loss
- Pretrained on COCO, fine-tuned on malaria dataset
- Purpose: Object detection and classification of malaria cell types in blood smear images
- Class Balancing: Oversampling and per-class loss weighting

### Inputs
- RGB microscopy images of Giemsa-stained human blood smears
- Image size: variable (resized and normalized during preprocessing)

### Outputs
- Bounding boxes for detected cells
- Class labels: red blood cell, trophozoite, ring, difficult, schizont, gametocyte, leukocyte
- Confidence scores for each detection

### Training Details
- Hardware: GPU-accelerated (CUDA support)
- Epochs: 60
- Optimizer: SGD (learning rate: 0.0001, momentum: 0.9, weight decay: 0.0005)
- Data Augmentation: Horizontal/vertical flips, brightness/contrast, affine transforms, color jitter, normalization
- Transfer Learning: Pretrained on COCO, fine-tuned on malaria dataset
- Loss Weighting: Class weights inversely proportional to class frequency

## Intended Uses
### Applications
- Automated detection and classification of malaria cell types (e.g., red blood cells, trophozoites, rings, schizonts, gametocytes, leukocytes, difficult cases) in blood smear images
- Assisting malaria diagnosis and research

### Domain & Users
- Dataset is only available for Non-commercial use, share-alike—just credit the source! which is released under Attribution-NonCommercial-ShareAlike 3.0 IGO license. See the Kaggle dataset page for license details https://www.kaggle.com/datasets/orvile/p-vivax-malaria-infected-human-blood-smears. 

### Out-Of-Scope Applications
- Detection of non-malaria parasites or other diseases
- Use on non-Giemsa-stained or non-blood-smear images
- Use as a sole diagnostic tool without human oversight

### License
CC BY-NC-SA 4.0 https://creativecommons.org/licenses/by-nc-sa/4.0/deed.en
Attribution-NonCommercial-ShareAlike 4.0 International

## Limitations
Not intended for direct clinical diagnosis without expert review. Performance may vary on images from different sources or staining protocols. Models are trained on the dataset which is only available for Non-commercial use, share-alike—just credit the source! which is released under Attribution-NonCommercial-ShareAlike 3.0 IGO license. See the Kaggle dataset page for license details https://www.kaggle.com/datasets/orvile/p-vivax-malaria-infected-human-blood-smears.

### Presence of Attributes
- Class Imbalance: Despite oversampling and weighting, rare cell types remain challenging due to dataset composition. May underperform on rare classes if class imbalance is extreme.
- Generalization: Model performance may drop on images with different staining, resolution, or from other labs.
- Clinical Use: Not validated for clinical deployment; expert review is required for diagnostic decisions.
- Improvement: Further balancing (e.g., cropping images to reduce red blood cell dominance) and more diverse data are recommended. Requires high-quality annotations
- Model performance may degrade on images with poor staining, low resolution, or artifacts

### Inputs
- Requires high-quality, annotated microscopy images
- Not robust to images outside the training domain

### Environment
- Designed for digital pathology settings; not validated for mobile or edge devices
- Not validated for clinical deployment; expert review is required for diagnostic decisions.

### Trade-offs
- Focal loss models may require more hyperparameter tuning
- Weighted loss models may underperform on extremely rare classes
- v2 models offer improved accuracy at the cost of slightly higher computational requirements

## Factors and Subgroups
### Instrumentation
- Refer to https://www.kaggle.com/datasets/orvile/p-vivax-malaria-infected-human-blood-smears for details

### Environments
- Refer to https://www.kaggle.com/datasets/orvile/p-vivax-malaria-infected-human-blood-smears for details

### Attributes
- Class imbalance: red blood cells are the majority class
- Minority classes: parasite stages and leukocytes

### Groups
- Model performance may vary across different patient populations, staining protocols, and imaging devices

## Metrics
### Model Performance Metrics
- Precision
- Recall
- F1 Score
- Accuracy

### Evaluation Metrics
- Per-class and overall metrics reported on held-out test set
- Comparison across models for each metric

## Evaluation
All models were evaluated on a held-out test set of annotated blood smear images. Performance was measured using precision, recall, F1 score, accuracy, and mAP. Focal loss and v2 FPN models generally showed improved performance on minority classes and overall detection accuracy.

## Datasets and Results
- **Dataset:** P. vivax malaria-infected human blood smears (Kaggle) [P. vivax Malaria Infected Human Blood Smears (Kaggle)](https://www.kaggle.com/datasets/orvile/p-vivax-malaria-infected-human-blood-smears)
- **Classes:** red blood cell, trophozoite, ring, difficult, schizont, gametocyte, leukocyte
- **Preprocessing:** Data augmentation, normalization, weighted sampling

    ### Evaluation Results Comparison on Test Dataset

    | Model Name                                      | Precision  | Recall  | F1 Score  | Accuracy  |
    |-------------------------------------------------|------------|---------|-----------|-----------|
    | faster-rcnn-resnet50-fpn-weighted-CE-loss       | 0.902      | 0.918   | 0.910     | 0.835     |
    | faster-rcnn-resnet50-fpn-weighted-focal-loss    | 0.902      | 0.930   | 0.916     | 0.845     |
    | faster-rcnn-resnet50-fpn-v2-weighted-CE-loss    | 0.885      | 0.938   | 0.911     | 0.836     |
    | faster-rcnn-resnet50-fpn-v2-weighted-focal-loss | 0.885      | 0.931   | 0.908     | 0.831     |

    *Minority Class F1 refers to the average F1 score across rare cell types (trophozoite, ring, schizont, gametocyte, leukocyte, difficult).  
    v2 and focal loss models show improved performance, especially on minority classes.*

## Release Notes
### Variants
- Four model variants released:
    - faster-rcnn-resnet50-fpn-weighted-CE-loss
    - faster-rcnn-resnet50-fpn-weighted-focal-loss
    - faster-rcnn-resnet50-fpn-v2-weighted-CE-loss
    - faster-rcnn-resnet50-fpn-v2-weighted-focal-loss
- All models trained and evaluated on the same dataset and metrics
- Code, training details (including loss and ROC curve visulization charts) and evaluation results (including Confusion Matrix, Precision, Recall, F1 Score, Accuracy and Visulizaions for cell detection and classification) are available in corresponding Jupyter notebooks

### Model Maintainance & Updates
These 4 models will be maintained by Junept Limited as required.

## References

- [Fast R-CNN (Girshick, 2015)](https://arxiv.org/abs/1504.08083)
- [Faster R-CNN (Ren et al., 2016)](https://arxiv.org/abs/1506.01497)
- [Focal Loss for Dense Object Detection (Lin et al., 2017)](https://arxiv.org/abs/1708.02002)
- [Benchmarking Detection Transfer Learning with Vision Transformers (Li et al., 2021)](https://arxiv.org/abs/2111.11429)


## Definitions
- **FPN:** Feature Pyramid Network, a backbone enhancement for multi-scale detection
- **Weighted Cross-Entropy Loss:** Loss function that applies higher weights to rare classes
- **Focal Loss:** Loss function that focuses training on hard, misclassified examples
- **mAP:** Mean Average Precision, a standard object detection metric
- **COCO:** Common Objects in Context, a large-scale object detection dataset used for pretraining

**Note:** For reproducibility, see the full notebook for code, configuration, and detailed results.
