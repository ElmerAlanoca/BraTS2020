# BraTS2020

**Dataset Information**

![BraTS2020](https://user-images.githubusercontent.com/42582941/179636170-d89edabe-1daf-4eb0-a78c-204f8c441039.JPG)

https://www.kaggle.com/datasets/awsaf49/brats20-dataset-training-validation

- Multimodals scans available as NIfTI files (.nii.gz)

- Four channels of information:

    Native(T1)
    
    Post-contrast T1-weighted (T1CE)
    
    T2-weighted (T2)
    
    T2 Fluid Attenuated Inversion Recovery (FLAIR) volumes
    

- All the imaging datasets have been segmented manualy and were approved by experienced neuro-rediologists.

- Annotatios (labels):

    Label 0: Unabeled volume
    
    Label 1: Necrotic and non-enhancing tumor core (NCR/NET)
    
    Label 2: Peritumora edema (ED)
    
    Label 3: Missing (No pixels i all the volumes contain label 3)
    
    Label 4: GD-enhancing tumor (ET)
    
**Our Approach**

**Step 1: Get the data reday.**

- Download the dataset and unzip it.

- Segmented file name in Folder 355 has a weird name. Rename it to match others.

- Install nibabel library to handle nii files (https://pypi.org/project/nibabel/)

- Scale all volumes (using MinMaxScaler).

- Combine the three non-native volumes (T2, T1CE and Flair) into a single multi-channel volume.

- Reassign pixels of value 4 to value 3 (as 3 is missing from original labels).

- Crop volumnes to remove useless blank regions around the actual volume of interest (Crop to 128x128x128).

- Drop all the volumes where the amount of annotated data is less that certain percentage. (To maximize training on real labeled vo0lumes).

- Save all useful volumes to the local drive as numpy arrays (npy).

- Split image and mask volumes into train and validation datasets.

**Step 2: Define custom data generator.**

- Keras image data generator only works with jpg, png, and tif images. It will not recognize np files. We need to define a custom generator to load our data from the disk.

**Step 3: Define the 3D U-net model.**

- Extend the standard 2D U-net into 3D OR.

- Copy the code from online OR.

- Use 3D segmentation models library.

**Step 4: Train and Predict.**

- Train by loading images in batches using our custom generator.
