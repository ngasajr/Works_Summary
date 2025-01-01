# Summary of *Multimodal Physiological Signal Emotion Recognition Based on Convolutional Recurrent Neural Network* by Jinxiang Liao et al.

---

## Introduction

The study addresses the challenge of improving emotion recognition accuracy using physiological signals, particularly EEG (Electroencephalogram) and peripheral physiological signals (EOG, EMG, GSR, RSP, BVP, and TMP). Prior research has largely focused on single-modal data for emotion recognition, which limits classification accuracy. To overcome this, the authors propose a novel method based on Convolutional Neural Networks (CNN) and Long Short-Term Memory (LSTM) networks. CNN is employed to capture the spatial characteristics of EEG signals, while LSTM is used to model the temporal representations of peripheral physiological signals. The combination of these modalities is aimed at improving recognition accuracy in the emotional dimensions of arousal and valence.

**Takeaway**: This paper proposes a deep learning approach combining CNN for spatial feature extraction and LSTM for temporal representations, improving multi-modal physiological emotion recognition accuracy.

---

## Methods

### Data Preprocessing and EEG Signal Transformation

The authors utilized the DEAP dataset, which provides EEG and peripheral physiological signals recorded during participants' exposure to emotionally stimulating music videos. The EEG signals were converted from one-dimensional sequences into two-dimensional matrices to capture spatial relationships between different regions of the brain. These matrices were normalized to reduce signal variability.

### CNN for Spatial Feature Extraction

The 2D CNN architecture was applied to the EEG matrices to extract spatial features. Three convolutional layers with batch normalization were used, avoiding pooling to prevent information loss. The final output was a feature vector representing the spatial characteristics of the EEG signals.

### LSTM for Temporal Feature Extraction

The LSTM network was used to model temporal dependencies in the peripheral physiological signals. Two stacked LSTM layers captured temporal patterns, and the resulting feature vectors were concatenated with the spatial features from the EEG signals to form a comprehensive multi-modal representation.

**Takeaway**: The method involves using CNN for spatial features and LSTM for temporal features, combining these for emotion classification.

---

## Experiment and Results

### Dataset: DEAP

The DEAP dataset was used, containing EEG and peripheral signals from 32 participants. The signals were preprocessed, and the data was segmented into 1-second intervals.

### Classification Performance

The CNN-LSTM model achieved high performance in both arousal and valence dimensions:

- EEG classification: 89.68% (arousal) and 89.19% (valence).
- Peripheral signals classification: 63.06% (arousal) and 62.41% (valence).
- Combined model: 93.06% (arousal) and 91.95% (valence).

**Takeaway**: The combination of EEG and peripheral physiological signals improves emotion recognition accuracy, achieving over 93% in arousal classification.

---

## Conclusion

The method proposed in this paper improves emotion recognition performance by combining spatial features from EEG and temporal features from peripheral signals. Future work will focus on optimizing channel selection for further improvements.

**Takeaway**: Fusing spatial and temporal features from multi-modal physiological signals significantly enhances emotion recognition accuracy.

---
