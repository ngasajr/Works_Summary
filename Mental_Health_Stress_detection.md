
# Big Picture Overview of my codes below

The multimodal stress detection pipeline. The general workflow is:

<p align="center">
  <img src="https://github.com/ngasajr/Works_Summary/blob/main/Material/Arch_multimodal_stress_wesad_.png" width="800" />
</p>


---

The following order was used to prepare data and extract features from the latent layer of autoencoder model: </br>
1. Preprocessing and merging subject data
</br>Command: <br>
python merge_subj_data.py
</br></br>
Input data path: 'data/WESAD/'</br>
The command execute codes to generates the following files in data folder:</br>
subj_merged_acc_w.pkl</br>
subj_merged_bvp_w.pkl</br>
subj_merged_eda_temp_w.pkl</br>
merged_chest_fltr.pkl</br></br>
2. Creating autoencoder model and extracting latent features
</br>Command: </br>
python extract_ae_latent_features.py
</br></br>
Input files:<br>
subj_merged_acc_w.pkl</br>
subj_merged_bvp_w.pkl</br>
subj_merged_eda_temp_w.pkl</br>
merged_chest_fltr.pkl</br>
  - Uses ae_feature_extractor.py to build and training autoencoder model and extract features. </br>
  - Saving extracted features leaving one subject out into pickle files in features/train and features/test directories. The number in the filename indicates which subject was left out in each fold.</br></br>
3. SVM_classifier.ipynb - Building SVM classifier that uses latent features extracted by autoencoder for three class classification of WESAD dataset: neutral, stress, and ammusement. Results analysis can be seen in the codes file.</br></br>
4. MLP_classifier.ipynb - Building MLP (Multi Layer Perceptron) classifier that uses latent features extracted by autoencoder for three class classification of WESAD dataset: neutral, stress, and ammusement. Results analysis can be seen in the codes file.

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

## Reviewed work's Workflows

Architectures Visualization:

<p float="left">
  <img src="https://github.com/ngasajr/Works_Summary/blob/main/Material/Hierarchical_Puzzle_Learning_Machine.PNG" width="500" />
  <img src="https://github.com/ngasajr/Works_Summary/blob/main/Material/Shuffled_ECA_Net.PNG" width="400" />
  
</p>

---

**Refferences:**
- [WESAD Datasets](https://archive.ics.uci.edu/dataset/465/wesad+wearable+stress+and+affect+detection)
- [Hierachical Puzzle Learning Machine](https://www.sciencedirect.com/science/article/pii/S1746809423000575)
- [Shuffled_ECA_Net](https://www.sciencedirect.com/science/article/pii/S0010482524013027)
  
---
