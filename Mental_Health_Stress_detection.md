
# Big Picture Overview of my codes below

The multimodal stress detection pipeline. The general workflow is:

---

## Data Preparation :

Extracting sensor data (e.g., ECG, EDA) from multiple subjects in the WESAD dataset.
Merging the data for each sensor type into consolidated files for easier processing.

## Feature Extraction :

Using an Autoencoder to extract features from the sensor data.
The Autoencoder learns a compressed representation of the input data, reducing dimensionality while retaining important information.

## Feature Fusion :

Combining extracted features from multiple sensors (e.g., ECG, EDA, EMG) into a single feature matrix.
Applying a custom attention mechanism (Shuffled ECA Module) for further feature fusion based on attention mechanism

## Classification :

Using a Convolutional Neural Network (CNN) for classification.
The target is to classify data into three categories: Neutral, Stress, and Amusement.

## Evaluation and Visualization :

Evaluating the model using accuracy, F1-score, and a confusion matrix.
Visualizing the confusion matrix to interpret model performance.

---

### TBD

| TBD              | TBD                         |TBD                 |
|-----------------------|--------------------------------------------|------------------------------------------|
| TBD     | TBD  | TBD     |
| TBD      | TBD        | TBD                     |
| TBD  | TBD                         | TBD  |
| TBD           | TBD     | TBD             |
| TBD       | TBD                 | TBD                       |
| TBD       | TBD              | TBD            |

---

### Overview, Progress, and Plan

TBD

---

**Refference:**
- [WESAD Datasets](https://archive.ics.uci.edu/dataset/465/wesad+wearable+stress+and+affect+detection)
  
---
