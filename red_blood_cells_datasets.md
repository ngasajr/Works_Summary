# Dataset Name: BCCD (Blood Cell Count and Detection) Dataset | Complete Blood Count (CBC) Dataset
-------------------------------------------------------------------------------------------------------------------------------------------------


Sample Visualization:

<p float="left">
  <img src="https://github.com/Shenggan/BCCD_Dataset/blob/master/BCCD/JPEGImages/BloodImage_00000.jpg" width="300" />
  <img src="https://github.com/Shenggan/BCCD_Dataset/blob/master/BCCD/JPEGImages/BloodImage_00345.jpg" width="300" /> 
  <img src="https://github.com/Shenggan/BCCD_Dataset/blob/master/BCCD/JPEGImages/BloodImage_00090.jpg" width="300" />
  
</p>
<p float="left">
  <img src="https://github.com/Shenggan/BCCD_Dataset/blob/master/BCCD/JPEGImages/BloodImage_00135.jpg" width="300" />
  <img src="https://github.com/Shenggan/BCCD_Dataset/blob/master/BCCD/JPEGImages/BloodImage_00180.jpg" width="300" />
  <img src="https://github.com/Shenggan/BCCD_Dataset/blob/master/BCCD/JPEGImages/BloodImage_00225.jpg" width="300" />
 
</p>
<p float="left">
  <img src="https://github.com/Shenggan/BCCD_Dataset/blob/master/BCCD/JPEGImages/BloodImage_00270.jpg" width="300" />
  <img src="https://github.com/Shenggan/BCCD_Dataset/blob/master/BCCD/JPEGImages/BloodImage_00315.jpg" width="300" />
  <img src="https://github.com/Shenggan/BCCD_Dataset/blob/master/BCCD/JPEGImages/BloodImage_00360.jpg" width="300" />
 
</p>


## 📖 Project Goal

BCCD Dataset is a small-scale dataset for blood cell detection. 


## 📖 Overview of dataset

The dataset contains 400 blood smear images along with their annotation files. Each image is resized to ```640 x 480``` resolution. 

Datasets have three kinds of labels :
  * RBC (Red Blood Cell)
  * WBC (White Blood Cell)
  * Platelets

From this [dataset](https://github.com/Shenggan/BCCD_Dataset), [nicolaschen1](https://github.com/nicolaschen1) developed two Python scripts to make preparation data (CSV file and images) for recognition of abnormalities in blood cells on medical images.

- export.py: it creates the file "test.csv" with all data needed: filename, class_name, x1,y1,x2,y2.
- plot.py: it plots the boxes for each image and save it in a new directory.

<p align="center">
  <img src="https://github.com/Shenggan/BCCD_Dataset/blob/master/example.jpg" width="400">
</p>



# Chula RBC-12-Dataset
-------------------------------------------------------------------------------------------------------------------------------------------------


Sample Visualization:

<p float="left">
  <img src="https://github.com/Chula-PIC-Lab/Chula-RBC-12-Dataset/blob/main/Dataset/141.jpg" width="300" />
  <img src="https://github.com/Chula-PIC-Lab/Chula-RBC-12-Dataset/blob/main/Dataset/206.jpg" width="300" /> 
  <img src="https://github.com/Chula-PIC-Lab/Chula-RBC-12-Dataset/blob/main/Dataset/273.jpg" width="300" />
  
</p>
<p float="left">
  <img src="https://github.com/Chula-PIC-Lab/Chula-RBC-12-Dataset/blob/main/Dataset/258.jpg" width="300" />
  <img src="https://github.com/Chula-PIC-Lab/Chula-RBC-12-Dataset/blob/main/Dataset/306.jpg" width="300" />
  <img src="https://github.com/Chula-PIC-Lab/Chula-RBC-12-Dataset/blob/main/Dataset/313.jpg" width="300" />
 
</p>
<p float="left">
  <img src="https://github.com/Chula-PIC-Lab/Chula-RBC-12-Dataset/blob/main/Dataset/339.jpg" width="300" />
  <img src="https://github.com/Chula-PIC-Lab/Chula-RBC-12-Dataset/blob/main/Dataset/716.jpg" width="300" />
  <img src="https://github.com/Chula-PIC-Lab/Chula-RBC-12-Dataset/blob/main/Dataset/84.jpg" width="300" />
 
</p>


## 📖 Project Goal

Red Blood Cell Segmentation with Overlapping Cell Separation and Classification from an Imbalanced Dataset. 


## 📖 Overview of dataset

Chula-RBC-12 Dataset is a dataset of red blood cell (RBC) blood smear images containing 12 classes of RBC types consisting of 706 smear images that contain over 20,000 RBC cells. The dataset was collected at the Oxidation in Red Cell Disorders Research Unit, Chulalongkorn University in 2019 using a DS-Fi2-L3 Nikon microscope at 1000x magnification.

RBC Types
  * 0 Normal cell
  * 1 Macrocyte
  * 2 Microcyte
  * 3 Spherocyte
  * 4 Target cell
  * 5 Stomatocyte
  * 6 Ovalocyte
  * 7 Teardrop
  * 8 Burr cell
  * 9 Schistocyte
  * 10 uncategorised
  * 11 Hypochromia
  * 12 Elliptocyte

The "Dataset" folder contains 738 RBC blood smear images with 640*480 resolution.
The "Label" folder contains label data with the name of the corresponding image. The file can contain multiple lines. Each line is stored in the following sequence:
  - x coordinate
  - y coordinate
  - type of RBC in number


# PathOlOgics_RBCs Cells-Dataset
-------------------------------------------------------------------------------------------------------------------------------------------------

Dataset posted on 2023-09-13, authored by [AhmedElsafty](https://github.com/ssafty)

Sample Visualization:

<p float="left">
  <img src="https://github.com/ngasajr/Tutorial/blob/main/Works_Summary/Ahmed/rounded_rbc.png" width="200" />
  <img src="https://github.com/ngasajr/Tutorial/blob/main/Works_Summary/Ahmed/Ovalocytes.png" width="200" /> 
  <img src="https://github.com/ngasajr/Tutorial/blob/main/Works_Summary/Ahmed/Teardrops.png" width="200" />
  
</p>
<p float="left">
  <img src="https://github.com/ngasajr/Tutorial/blob/main/Works_Summary/Ahmed/Three_Overlapping_RBCs.png" width="200" />
  <img src="https://github.com/ngasajr/Tutorial/blob/main/Works_Summary/Ahmed/Two_Overlapping_RBCs.png" width="200" />
  <img src="https://github.com/ngasajr/Tutorial/blob/main/Works_Summary/Ahmed/Fragmented_RBCs.png" width="200" />
 
</p>
<p float="left">
  <img src="https://github.com/ngasajr/Tutorial/blob/main/Works_Summary/Ahmed/Burr_Cells.png" width="200" />
  <img src="https://github.com/ngasajr/Tutorial/blob/main/Works_Summary/Ahmed/Borderline_Ovalocytes.png" width="200" />
  <img src="https://github.com/ngasajr/Tutorial/blob/main/Works_Summary/Ahmed/Angled_Cells.png" width="200" />
 
</p>


## 📖 Project Goal

The aim of creating these datasets was to facilitate the development of a generalizable automated system for RBCs classification utilizing the current DL technology or any other advanced technologies that may evolve in the coming decades. 


## 📖 Overview of dataset

PathOlOgics_RBCs Cells Dataset contains a total of 240,790 cells. It is represented by its cropped image, mask, and segmented image, all subjected to meticulous processing and individual scrutiny by the hematologists, ensuring adherence to rigorous scientific standards.

Within each of these primary folders, there are nine subfolders, meticulously dedicated to each RBCs class, encompassing the following counts of cells:
  * Angled cells: 24,187
  * Borderline ovalocytes: 35,540
  * Burr cells: 8,948
  * Fragmented RBCs: 7,186
  * Ovalocytes: 55,348
  * Rounded RBCs: 46,346
  * Teardrops: 16,298
  * Three-overlapping RBCs: 15,577
  * Two-overlapping RBCs: 31,360
    
The naming scheme for the cropped image, mask, and segmented image of every cell adheres to a consistent format, starting with the slide/smear number, followed by the unique patch number, and concluding with the XYWH notation, accurately specifying the position on the patch. All these images are conveniently stored in the ".jpg" format.

