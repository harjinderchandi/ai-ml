# Malaria Cell Detection Models: General Audience Overview

This project uses four advanced artificial intelligence models to automatically detect and classify different types of cells in images of human blood smears. The models are trained to recognize red blood cells and several malaria parasite stages, helping to speed up and improve malaria diagnosis. By analyzing thousands of images, these models learn to spot patterns that may be hard for the human eye to catch. The results show that the models can accurately identify both common and rare cell types, making them a valuable tool for medical professionals and researchers fighting malaria.

## Model Variants
- Four model variants released:
    - faster-rcnn-resnet50-fpn-weighted-CE-loss
    - faster-rcnn-resnet50-fpn-weighted-focal-loss
    - faster-rcnn-resnet50-fpn-v2-weighted-CE-loss
    - faster-rcnn-resnet50-fpn-v2-weighted-focal-loss
- All models trained and evaluated on the same dataset and metrics
- Code, training details (including loss and ROC curve visulization charts) and evaluation results (including Confusion Matrix, Precision, Recall, F1 Score, Accuracy and Visulizaions for cell detection and classification) are available in corresponding Jupyter notebooks

## Model Card
Please refer to **model-card.md** file 

## Model Datasheet
Please refer to **model-datasheet.md** file