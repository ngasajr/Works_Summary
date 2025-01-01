# Summary of *ECG and EEG based detection and multilevel classification of stress using machine learning for specified genders: A preliminary study*
**Accepted: October 10, 2023**
**Published: October 11, 2023**   

**https://pmc.ncbi.nlm.nih.gov/articles/PMC10473514/**

---

## Introduction

This study presents a novel approach to stress detection and classification using both ECG (Electrocardiogram) and EEG (Electroencephalogram) signals. Unlike prior work, which often focuses on single modalities, this research explores how combining these two physiological signals can improve accuracy. Additionally, the study considers gender differences in stress response, noting that females, particularly in different phases of the menstrual cycle, may exhibit different physiological reactions to stress than males. 

**Takeaway**: This research presents a novel multi-modal, gender-specified approach to stress detection, addressing gaps in existing machine learning models for physiological stress detection.

---

## Methods

### Data Collection

The dataset was collected from 40 participants, including 21 females and 19 males. EEG and ECG data were recorded while participants performed stress-inducing tasks. 

### Feature Extraction

The authors extracted several features from both EEG and ECG data. For the ECG, heart rate variability (HRV) features were computed in both time and frequency domains. EEG data were processed into frequency bands, and interhemispheric asymmetry was calculated for various brain regions.

### Model Development

A variety of machine learning classifiers were applied to the feature sets. These included Naive Bayes (NB), Support Vector Machines (SVM), k-Nearest Neighbor (kNN), Random Forest (RF), and Adaptive Boosting (AdaBoost).

**Takeaway**: The methodology used a combination of well-established machine learning techniques on a variety of ECG and EEG features to detect and classify stress, with special attention paid to gender differences.

---

## Results

### Stress Detection

The highest accuracy for stress detection was achieved using kNN and SVM classifiers. The inclusion of EEG data boosted the accuracy significantly, with accuracies reaching 87.58% for males and 92.70% for females using SVM and RBF-SVM.

### Multilevel Stress Classification

The stacking technique improved classification accuracy across genders, achieving 64.08% accuracy for mixed genders, 62.60% for females, and 71.57% for males.

**Takeaway**: The combination of EEG and ECG data significantly improved stress detection accuracy, with gender-specified models outperforming gender-neutral ones.

---

## Conclusion

This study demonstrated the effectiveness of combining ECG and EEG signals for stress detection and classification. The results suggest that integrating multimodal data significantly enhances the classification of stress, especially in gender-specified models.

**Takeaway**: This paper provides a strong foundation for future work in multi-modal, gender-sensitive stress detection using machine learning.

---

## Repository to Check

This repository introduces MentaLLaMA, the first open-source instruction following large language model for interpretable mental health analysis.**https://github.com/SteveKGYang/MentalLLaMA**

