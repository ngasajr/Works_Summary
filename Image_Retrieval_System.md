
# Project Report: Image Retrieval System

---

## Objective

The primary objective of this project is to create an Image Retrieval System that can efficiently 
find visually similar images from a collection based on a query image. The system leverages advanced 
machine learning techniques, including deep feature extraction with Vision Transformers (ViT), and 
scalable similarity search using FAISS (Facebook AI Similarity Search).

## Project Description :

The project consists of three main modules:

1. **Feature Extraction** (feature_extractor.py): </br>
  - Uses a **Vision Transformer (ViT)** model, specifically vit_base_patch16_224 from the timm 
  library, to extract high-dimensional feature embeddings from images. </br>
  - Each image is processed into a numerical vector (768-dimensional for ViT-B/16) 
  that captures its visual characteristics.</br>
  - Preprocessing steps include resizing, normalization, and transformation of images 
  into a tensor format compatible with the ViT model.</br></br>


2. **Indexing and Metadata Storage** (retrieval_system.py): </br>
   - Extracts features from all images in a directory.</br>
   - Stores these features in a FAISS index for efficient similarity search.</br>
   - Maintains a metadata file that maps indexed vectors to their respective image paths, 
   filenames, and indexing timestamps.</br></br>

3. **Main Control and User Interface** (index_and_retrieve.py):</br>
   - Provides a user-friendly interface to:</br>
       - Index new images into the retrieval system.</br>
       - Search for images similar to a query image.</br></br>
   - Automatically calculates optimal settings for indexing based on the size of the 
   image dataset (e.g., number of regions/clusters).</br>
   - Pretty prints the results, including filenames, full paths, and similarity scores.</br></br>

## Key Features :

1. **Deep Learning-Based Feature Extraction:** </br>
  - Utilizes pre-trained Vision Transformers for accurate feature extraction. </br>
  - Highly effective at capturing complex visual patterns in images.</br></br>

2. **Efficient Similarity Search:** </br>
   - Uses **FAISS IndexIVFFlat** for scalable and approximate nearest-neighbor searches.</br>
   - Supports fast queries even on large datasets by dividing the feature space into clusters and searching only within relevant clusters.</br></br>

3. **Device Flexibility:** </br>
   - Automatically detects and utilizes GPU resources for faster computations if available.</br>
   - Falls back to CPU gracefully if GPU support is unavailable.</br></br>

4. **Error Handling and Logging:** </br>
   - Provides detailed logs and error messages to assist in debugging and 
   system monitoring.</br></br>

5. **Customizability:** </br>
   - Allows users to adjust indexing and search parameters, such as the number of clusters (n_regions) and the number of clusters to search (nprobe).</br></br>

## Applications:

The Image Retrieval System is highly versatile and can be applied across various domains, including:

1. **Business and E-commerce:**</br>
   - **Visual Search Engines:** Allow customers to upload a product image and find similar items in an online catalog.</br>
   - **Recommendation Systems:** Suggest visually similar products to customers based on their browsing history.</br></br>

2. **Finance:**</br>
   - **Document Similarity:** Identify visually similar financial documents or charts for fraud detection or trend analysis.</br></br>

3. **Security:**</br>
   - **Surveillance Systems:** Match faces or objects in real-time video feeds with a database of known individuals or objects.</br>
   - **Forensic Analysis:** Locate evidence from large datasets of images or videos.</br></br>

4. **Healthcare:**</br>
   - **Medical Image Analysis:** Retrieve similar X-rays, MRIs, or CT scans to assist in 
   diagnosis.</br>
   - **Pathology:** Compare histopathological slides to identify patterns of disease.</br></br>

5. **Education and Research:**</br>
   - **Dataset Management:** Organize and search through large datasets of images for academic research.</br>
   - **Art and Design:** Identify artwork or design elements similar to a given image.</br></br>

6. **Social Media and Content Platforms:**</br>
   - **Content Moderation:** Detect visually similar inappropriate or copyrighted content.</br>
   - **Photo Tagging and Organization:** Automatically group similar photos for better organization.</br></br>


## Advantages:

1. **Scalability:**</br>
   - FAISS indexing enables efficient searches across millions of images.</br>
   - Cluster-based indexing reduces computational overhead while maintaining accuracy.</br></br>

2. **Accuracy:**</br>
   - Deep learning-based feature extraction ensures high-quality embeddings for robust similarity detection.</br></br>

3. **Speed:**</br>
   - GPU acceleration and approximate search methods drastically reduce search times.</br></br>

4. **Ease of Use:**</br>
   - A straightforward interface for both indexing and searching makes it accessible to non-experts.</br></br>

## Future Enhancements

1. **Improved Feature Extraction:**</br>
   - Incorporate fine-tuning of the ViT model on domain-specific datasets to improve feature quality.</br>
   - Support for multimodal features (e.g., combining text and image features).</br></br>

2. **Advanced Indexing Techniques:**</br>
   - Use HNSW (Hierarchical Navigable Small World graphs) for even faster and more memory-efficient searches.</br>
   - Support for hybrid indexes combining different algorithms.</br></br>

3. **Real-Time Search:**</br>
   - Add support for streaming data to enable real-time image indexing and retrieval.</br></br>

4. **Cloud Integration:**</br>
   - Deploy the system in cloud environments for distributed indexing and global accessibility.</br></br>

5. **User-Friendly Interfaces:**</br>
   - Build a web or mobile interface for uploading query images and displaying results interactively.</br></br>

6. **Broader Application:**</br>
   - Integrate with APIs to allow businesses to embed the retrieval functionality into their platforms.</br></br>

## Conclusion </br>
The Image Retrieval System provides a powerful and flexible solution for managing and querying large collections of images. By combining state-of-the-art deep learning models with scalable similarity search techniques, it has the potential to transform workflows in a wide range of industries, enhancing efficiency and decision-making. Future enhancements can expand its applicability and usability, making it a cornerstone tool for image-based information retrieval.

## Workflow and Detailed Overview

1. **Feature Extraction** </br>
The process begins by extracting deep features from images using a pre-trained Vision Transformer (ViT) model, implemented with the timm library. The features are 768-dimensional vectors representing the visual characteristics of each image.
   - **Command:** </br>
   python feature_extractor.py




**Refferences:**
- [WESAD Datasets](https://archive.ics.uci.edu/dataset/465/wesad+wearable+stress+and+affect+detection)
- [Hierachical Puzzle Learning Machine](https://www.sciencedirect.com/science/article/pii/S1746809423000575)
- [Shuffled_ECA_Net](https://www.sciencedirect.com/science/article/pii/S0010482524013027)
  
---
