# Summary of *Inferring Social Media Users' Mental Health Status from Multimodal Information* by Xu, Z., Pérez-Rosas, V. and Mihalcea, R., 2020, May. 

**Proceedings of the 12th Conference on Language Resources and Evaluation (LREC 2020)**

---

## Introduction

The paper investigates the potential of using multimodal information from social media posts to detect mental health statuses. The authors propose a scalable method by analyzing social media data from platforms like Flickr, which provides rich multimodal data (images, captions, and metadata).

The authors focus on two tasks: classifying users as either healthy or suffering from a mental health condition, and identifying users prone to mental illness by analyzing the onset of mental illness-related tags. Their hypothesis is that combining multiple modalities (text, images, and metadata) will improve classification accuracy.

---

## Methods

### Data Collection

The dataset was collected from Flickr using hashtags related to mental illness. The final dataset consisted of three groups: users suffering from mental illness, users prone to mental illness, and healthy users.

### Multimodal Features

1. **Visual Features**: Low-level (color, brightness, texture) and high-level (scene attributes, faces) features were extracted from images.
2. **Linguistic Features**: Captions were analyzed for stylistic features and emotional content using LIWC.
3. **Metadata Features**: Post views and image editing metadata (exif data) were considered.

---

## Experiment and Results

### Classification Performance

The results showed that combining visual, linguistic, and metadata features yielded the best performance. Neural networks achieved the highest accuracy in detecting mental illness, with an F1 score of 0.85.

### Feature Analysis

Mentally ill users posted darker images with fewer faces and used more negative language. Healthy users posted more dynamic, bright images.

---

## Conclusion

The study demonstrates that multimodal social media data can be used to detect mental health status. The authors suggest further research to refine feature sets and explore applications in real-world mental health detection.

