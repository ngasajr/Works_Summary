# Summary of *Hierarchical Autoencoder Frequency Features for Stress Detection*

---
#### *Kuttala, Radhika, Ramanathan Subramanian, and Venkata Ramana Murthy Oruganti. "Hierarchical Autoencoder Frequency Features for Stress Detection." IEEE Access (2023).*

---

## Introduction

Stress, with its significant negative impacts on health, has become a critical social concern, making early detection essential for effective management. The paper presents a deep learning approach for stress detection using multimodal physiological signals, specifically Electrocardiogram (ECG) and Electrodermal activity (EDA). The novelty lies in the hierarchical autoencoder (AE) feature fusion in the frequency domain, combined with a CRNN-SE model.

Questionnaires were used to detect stress but are rarely used nowadays because of constraints, including time commitment, reliability, etc. Therefore, to overcome these limitations, stress is quantified using the various components of the stress response, such as behaviour, physiology, and psychology. Among these, physiological signals are regarded as reliable for detecting stress since deliberate human actions cannot influence them. Physiological measures such as electromyography (EMG), blood pressure, ECG, EDA, temperature, breathing frequency, respiration rate, electroencephalogram (EEG), etc., can be used to measure stress. 

A number of stress detection studies have demonstrated that, among these physiological signals, ECG and EDA are strong, reliable stress indicators when used independently and in combination. EDA indicates the skin’s electrical characteristics. Skin containing blood vessels and glands that sweat are exclusively controlled through the sympathetic branch. EDA is thus a perfect, unaffected way to quantify sympathetic activity. ECG has been regularly used to detect stress. Human stress can precisely be detected by monitoring an increase in heart rate and variations in Heart Rate Variability (HRV) measures, which can actively react to the buildup of mental pressure. Hence, studies have also concluded that ECG and EDA signals are sufficient to detect stress.

Stress detection using physiological signals can be combined with time-frequency, frequency and time-domain approaches. Most of the earlier studies prioritized preferring temporal domain over frequency domain analysis. Time-domain characteristics support physiological data that is subject-dependent, whereas frequency-domain features are good at differentiating between various levels of physical effort. Therefore, frequency domain features are more important than time domain features for subject-independent studies.

**Takeaway**: The work demonstrates improved stress detection through hierarchical autoencoder-based feature extraction, particularly for subject-independent analysis.

---

## Methodology

### Datasets

Four datasets were used: ASCERTAIN, CLAS, MAUS, and WAUC, each varying in data collection methods and participant tasks.

### Feature Engineering

- **DCT for Raw Data**: Conversion to the frequency domain.
- **Frequency Band Features**: PSD estimation with Welch's method, extracting 51 ECG and 40 EDA statistical features.

### Model Architecture

The hierarchical autoencoder extracted latent features, and the CRNN-SE model processed these for stress classification.

**Takeaway**: The combined use of hierarchical features and CRNN-SE enabled robust feature extraction and classification.

---

## Results

### Hierarchical Features

Enhanced performance using hierarchical fusion of autoencoder layers.

### Cost Function Comparison

MSE outperformed KL divergence and cosine similarity.

### Frequency Band vs. Raw Data

Frequency band features performed better by 4-8%.

### Generalizability

Consistent results across all datasets.

**Takeaway**: The method outperforms existing models, proving its efficacy and generalizability.

---

## Conclusion and Future Work

Hierarchical autoencoder frequency features proved effective for stress detection. Future research could include adding optimization constraints like sparsity and expanding data diversity.

**Takeaway**: A solid foundation for stress detection, with potential for future refinement.
