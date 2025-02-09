
# Project Name: Blood cells automation System

---

## Objective

Developing a comprehensive blood cell analysis platform that will be the system beyond just WBC classification but to include RBC and platelet counts, all types of classifications, diagnosis, lab analysis, education, and accurate captions. 

## Archtecture view:

Blood cells Automation System. The current general workflow is:

<p align="center">
  <img src="https://github.com/ngasajr/Works_Summary/blob/main/Material/llm_blood_cell_automation.png" width="800" />
</p>

---

## Potential structured implementation plan :

The project will go through the following implementations:

1. **Enhancing image captioning** (image_captioning_tool.py): </br>
  - Use a medical-specific model or fine-tune BLIP on blood cell datasets. </br>
  - Include terms like "smear", "staining", "artifacts", and specific cell morphologies.</br></br>

2. **Adding RBC and platelet detection/counting:** (rbc_platelet_count_tool.py): </br>
   - Train or use pre-trained object detection models for RBC and platelets.</br>
   - Handle overlapping cells with segmentation or watershed algorithms.</br></br>

3. **Develop classification models for RBC and platelets:** (rbc_platelets_classification_tool.py):</br>
   - Collect datasets for RBC morphology .</br>
       - sickle cells</br>
       - target cells</br>
       - etc.</br></br>
   - Classify platelets by size (giant platelets) or clumping.</br></br>

4. **Implement diagnostic logic:** (retrieval_system.py): </br>
   - Create a knowledge base of disorders linked to cell counts and morphologies.</br>
   - Use rules (e.g., if platelet count <150,000 suggest thrombocytopenia) or ML model.</br></br>

5. **Lab results analysis:** (lab_report_tool.py): </br>
   - OCR for uploaded lab reports.</br>
   - Parse numerical values and compare with image analysis results.</br></br>

6. **Educational content:** (retrieval_system.py): </br>
   - Build a database of explanations for each cell type and disorder.</br>
   - Use RAG to pull in the latest research or guidelines.</br></br>

7. **Improve LLM integration:** (retrieval_system.py): </br>
   - Structure prompts to include all analysis results.</br>
   - Use RAG with medical sources for accurate answers.</br>
   - Handle follow-up questions by maintaining conversation context.</br></br>

8. **Streamlit UI enhancements:** (retrieval_system.py): </br>
   - Display interactive reports with tabs for each analysis section.</br>
   - Visualizations like bar charts for cell counts, highlighted cells in images.</br></br>

**Possible challenges:**
  - Data availability: Annotated medical datasets for blood cells might be scarce. Look for public datasets like PBC (Peripheral Blood Cell) dataset, Raabin-WBC, etc.</br>
  - Computational resources: Running multiple models could require significant GPU memory. Optimize models or use cloud services.</br>
  - Clinical validation: Partnering with medical professionals to validate the system's accuracy and usefulness.</br></br>
    


**Refferences:**
- [WESAD Datasets](https://archive.ics.uci.edu/dataset/465/wesad+wearable+stress+and+affect+detection)
- [Hierachical Puzzle Learning Machine](https://www.sciencedirect.com/science/article/pii/S1746809423000575)
- [Shuffled_ECA_Net](https://www.sciencedirect.com/science/article/pii/S0010482524013027)
  
---
