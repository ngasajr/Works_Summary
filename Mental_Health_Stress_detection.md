
# WorkFlow, Detailed Overview

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

## Analysis of adopted Work with its Strengths and Potential Limitations

1. **Strengths:** </br>
  - **Comprehensive Multimodal Data:**  Work has approach of the use of chest and wrist sensor modalities with diverse signals (e.g., ECG, EDA, temperature, respiration) which ensures a rich dataset, critical for robust classification. </br>
  - **Leave-One-Subject-Out (LOSO) Cross-Validation:** With this evaluation method the approach ensures the model's generalizability across different individuals.</br>
  - **Autoencoder for Feature Extraction:** Using autoencoders for unsupervised feature extraction effectively reduces dimensionality and learns latent representations.</br>
  - **Diverse Classifiers:** Employing SVM and MLP classifiers that allows to compare performance across different model architectures.</br>
  - **Focus on Stress and Amusement Detection:** Including these psychological states addresses real-world mental health monitoring needs.</br></br>

2. **Potential Limitations:** </br>
  - **Limited Sensor Fusion Strategy:** The approach treats chest and wrist data separately, combining them only at the classifier stage. This might not fully exploit inter-modality relationships.</br>
  - **No Attention Mechanism:** The absence of attention-based methods might hinder the ability to focus on the most relevant features, which is increasingly critical in multimodal learning.</br>
  - **Manual Feature Selection for SVM:** While effective, manual feature engineering may be suboptimal compared to end-to-end learning.</br>
  - **Fixed Sampling Windows:** Fixed window sizes for preprocessing might miss finer temporal dynamics or introduce redundancy.</br></br>

---

## Proposed Approach01 :

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

## Archtecture view:

The multimodal stress detection pipeline. The general workflow is:

<p align="center">
  <img src="https://github.com/ngasajr/Works_Summary/blob/main/Material/Arch_multimodal_stress_wesad_.png" width="800" />
</p>

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

## Proposed Approach02 :

1. **Incorporating Attention-Based Sensor Fusion:** </br>
  - Integrate a **shuffled ECA module** into the adopted architecture for feature-level sensor fusion. This will allows the model to capture inter-modality relationships, enhancing performance.</br>
  - Example: Use attention to weigh features from different modalities (chest vs wrist) based on their relevance to stress detection.</br></br>

2. **Leverage Signal-to-Image Transformation:** </br>
  - Convert 1D physiological signals into 2D images using **wavelet scattering transforms** for feature extraction via pre-trained CNNs (e.g., ResNet152, InceptionV3)​</br></br>

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

## Key Takeaways from the Revised Papers

1. **Hierarchical Extreme Puzzle Learning Machine (HEPLM):**</br>
  - Converts physiological signals into 2D images using hybrid wavelet scattering and synchro-squeezing wavelet transform. </br>
  - Uses ResNet152 and InceptionV3 for feature extraction with ensemble learning.</br></br>

2. **Shuffled Efficient Channel Attention (ECA-Net):**</br>
  - Incorporates inter-modality attention, enabling advanced sensor fusion.</br>
  - Combines ECG, RESP, and EGG signals to achieve high accuracy (e.g., 0.916 F1-score)​</br></br>
---

**Refferences:**
- [WESAD Datasets](https://archive.ics.uci.edu/dataset/465/wesad+wearable+stress+and+affect+detection)
- [Hierachical Puzzle Learning Machine](https://www.sciencedirect.com/science/article/pii/S1746809423000575)
- [Shuffled_ECA_Net](https://www.sciencedirect.com/science/article/pii/S0010482524013027)
  
---
