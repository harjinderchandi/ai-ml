# Model Datasheet: Malaria Cell Detection and Classification

## Motivation
**For what purpose was the dataset created?**

The dataset was created to enable automated detection and classification of malaria-infected cells and other cell types in human blood smear images, supporting research and development of AI-based diagnostic tools. The specific task is object detection and classification of red blood cells, parasite stages, and leukocytes. The dataset fills a gap in annotated biomedical images for malaria research.

**Who created the dataset and on behalf of which entity?**

The dataset was created by researchers and contributors for the Kaggle competition "P. vivax malaria-infected human blood smears" (https://www.kaggle.com/datasets/orvile/p-vivax-malaria-infected-human-blood-smears). It is hosted on Kaggle and made available for research and educational purposes. Funding details are not specified. 

**Any other comments?**

The dataset is used in academic and applied research for malaria detection.


## Composition
**What do the instances represent?**

Each instance is a microscopy image of a Giemsa-stained human blood smear, annotated with bounding boxes and class labels for different cell types.

**How many instances of each type are in total?**

The dataset contains 1,328 blood smear images with 86,035 annotated objects, each with multiple annotated cells. The exact number of each class varies, with red blood cells being the majority.

**Is the dataset a sample of a larger set?**

The dataset is a sample of blood smear images and is not exhaustive. It is not fully representative of all global malaria cases but covers a diverse range of cell types and imaging conditions.

**What does each instance consist of?**

Each instance consists of a raw image and associated annotation data (bounding boxes and class labels).

**Are there any labels to the data?**

Yes, each cell in an image is labeled as one of: red blood cell, trophozoite, ring, difficult, schizont, gametocyte, or leukocyte.

**Is there any missing information from individual instances?**

Some images may have incomplete annotations or ambiguous cell types labeled as "difficult."

**Are relationships between individual instances made explicit?**

No explicit relationships between images; each is independent.

**Are there recommended data splits?**

Yes, typical splits are train/test, with rationale to ensure model generalization and unbiased evaluation.

**Is the dataset self-contained?**

Yes, all images and annotations are included in the dataset download from Kaggle.

**Does the dataset contain confidential data?**

No, the images are anonymized and do not contain personal or confidential information.

**Does the dataset contain potentially offensive or sensitive data?**

No, but some images may be visually uncomfortable for those unaccustomed to medical imagery.

**Does the dataset identify any subpopulations?**

No explicit demographic or subpopulation data is included.

**Is it possible to identify individuals from the dataset?**

No, the dataset is fully anonymized.

**Does the dataset contain sensitive data?**

Only health-related data (cell types in blood smears), but no personal identifiers.

**Any other comments?**

The dataset is intended for research and educational use.


## Collection process
**How was the data acquired?**

Images were collected from laboratory-prepared blood smears, digitized using microscopy, and annotated by experts.

**If the data is a sample, what was the sampling strategy?**

The dataset is a convenience sample, not strictly random, aiming to cover a range of cell types and infection stages.

**Over what time frame was the data collected?**

The specific time frame is not detailed in the Kaggle dataset documentation.

**Were there any ethical review processes?**

Not specified, but the dataset is anonymized and intended for research.

**Were individuals notified of the collection?**

Not applicable; no personal data is included.

**Did individuals consent to data collection?**

Not applicable; no personal data is included.

**If consent was obtained, was there a mechanism to revoke consent?**

Not applicable.

**Has a data protection impact analysis been conducted?**

Not specified.

**Any other comments?**

The dataset is publicly available for research.

## Preprocessing/cleaning/labelling
**Was any preprocessing/cleaning/labeling done?**

Yes, images were annotated with bounding boxes and class labels. Additional preprocessing (resizing, normalization, augmentation) is performed during model training.

**Was the raw data saved in addition to the processed data?**

Yes, raw images are included alongside annotation files.

**Any other comments?**

Preprocessing steps are documented in the project code and notebooks.


## Uses
**What other tasks could the dataset be used for?**

Cell segmentation, classification, biomedical image analysis, training other AI models for blood cell detection.

**Is there anything about the dataset that might impact future uses?**

- Dataset is only available for Non-commercial use, share-alike—just credit the source! which is released under Attribution-NonCommercial-ShareAlike 3.0 IGO license. See the Kaggle dataset page for license details https://www.kaggle.com/datasets/orvile/p-vivax-malaria-infected-human-blood-smears.
- Class imbalance (majority red blood cells) may affect model fairness. Users should be aware of potential bias and use class balancing techniques.

**Are there tasks for which the dataset should not be used?**

Not suitable for identifying individuals or for non-malaria-related diagnostics.

**Any other comments?**

The dataset is best used for research and educational purposes.


## Distribution
**Will the dataset be distributed to third parties?**

Yes, it is publicly available on Kaggle.

**How will the dataset be distributed?**

Downloadable from Kaggle under the dataset’s license.

**When will the dataset be distributed?**

It is already available.

**Will the dataset be distributed under a copyright or other IP license?**

Yes, see the Kaggle dataset page for license details. Typically, it is for research and educational use only.

**Any other comments?**

Users should review the Kaggle license before use.


## Maintenance
**Who will be maintaining the dataset?**

The original dataset is maintained by its Kaggle contributors and community.

**Any other comments?**

Updates or corrections may be made by the dataset maintainers on Kaggle.
