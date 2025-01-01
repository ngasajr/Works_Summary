# Background remover site | Upload and Download
-------------------------------------------------------------------------------------------------------------------------------------------------
## 📖 Website link

Remove the Image Background 100% Automatically and for Free.
[source](https://www.remove.bg/)


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
