# Malaria Cell Detection and Classification Models

This project uses four advanced artificial intelligence models to automatically detect and classify different types of cells in images of human blood smears. The models are trained to recognize red blood cells and several malaria parasite stages, helping to speed up and improve malaria diagnosis. By analyzing thousands of images, these models learn to spot patterns that may be hard for the human eye to catch. The results show that the models can accurately identify both common and rare cell types, making them a valuable tool for medical professionals and researchers fighting malaria.

## Data
P. vivax malaria-infected human blood smears (Kaggle) https://www.kaggle.com/datasets/orvile/p-vivax-malaria-infected-human-blood-smears

## Model
A deep learning model called **Faster R-CNN with Regional Propoasal Network (RPN) and RestNet 50 FPN Backnobe** is used to train the malaria detection model. This model uses a powerful image recognition technique called Fast R-CNN with a ResNet backbone, which helps it spot and classify different types of cells accurately. To make sure the model pays attention to rare cell types (not just the most common ones), it uses a special "weighted predictor." This means the model is trained to give extra importance to cell types that appear less often, helping it become fairer and more reliable for real-world malaria diagnosis.

- Four variants of the Faster R-CNN ResNet50 FPN were trained and evaluated as below:
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

## Hyperparameter Optimisation
- Epochs: 60
- Optimizer: SGD (learning rate: 0.0001, momentum: 0.9, weight decay: 0.0005)
- Details are documented in **model-card.md** file

## Results
 ### Evaluation Results Comparison on Test Dataset

    | Model Name                                      | Precision  | Recall  | F1 Score  | Accuracy  |
    |-------------------------------------------------|------------|---------|-----------|-----------|
    | faster-rcnn-resnet50-fpn-weighted-CE-loss       | 0.902      | 0.918   | 0.910     | 0.835     |
    | faster-rcnn-resnet50-fpn-weighted-focal-loss    | 0.902      | 0.930   | 0.916     | 0.845     |
    | faster-rcnn-resnet50-fpn-v2-weighted-CE-loss    | 0.885      | 0.938   | 0.911     | 0.836     |
    | faster-rcnn-resnet50-fpn-v2-weighted-focal-loss | 0.885      | 0.931   | 0.908     | 0.831     |
    |-------------------------------------------------|------------|---------|-----------|-----------|
  
  Details are documented in **model-card.md** file
  
## References of White Papers
- [Fast R-CNN (Girshick, 2015)](https://arxiv.org/abs/1504.08083)
- [Faster R-CNN (Ren et al., 2016)](https://arxiv.org/abs/1506.01497)
- [Focal Loss for Dense Object Detection (Lin et al., 2017)](https://arxiv.org/abs/1708.02002)
- [Benchmarking Detection Transfer Learning with Vision Transformers (Li et al., 2021)](https://arxiv.org/abs/2111.11429)

## Contact Details
Harjinder Chandi, Junept Limited

Email: harjinder.chandi@junept.co.uk

LinkedIn: https://www.linkedin.com/in/harjinder-chandi-53a1371a/
