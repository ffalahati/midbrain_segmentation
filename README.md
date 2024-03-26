# Segmentation of midbrain structures using nnU-Net and multi-sequence MRI data

This repository contains trained deep learning networks for the segmentation of key midbrain nuclei, the subthalamic nucleus (STN), substantia nigra (SN), and red nucleus (RN). The networks are based on the [nnU-Net](https://github.com/MIC-DKFZ/nnUNet/tree/nnunetv1) framework. 
The networks are trained using multi-sequence MRI data, specifically, T1-weighted, T2-FLAIR, and Quantitative Susceptibility Mapping (QSM) images. 
The networks are trained on 40 brain images, where the nuclei were manually traced on for each nucleus on QSM images.

For more information, please read [this paper]():
Falahati F., Gustavsson J., Kalpouzos G. (2024). Automated segmentation of midbrain nuclei using deep learning and multisequence MRI: a longitudinal study on iron accumulation with age. [Manuscript in preparation]

# Trained networks
The trained networks could be downloaded from this [link](https://1drv.ms/u/s!Ai108NIExicshy-jF9FlZvhL515W?e=2tEFvR).
There are two trained networks, the first network is trained with QSM and FLAIR images. The second Network is trained with QSM and T1 images. 

# Using the networks 
In order to use the networks, [nnU-Net-v1](https://github.com/MIC-DKFZ/nnUNet/tree/nnunetv1) library should be installed. 
The installation instructions are described [here](https://github.com/MIC-DKFZ/nnUNet/tree/nnunetv1#installation).   
Following a successful installation of the nnU-Net package, the data should be structured in [specific format](https://github.com/MIC-DKFZ/nnUNet/blob/nnunetv1/documentation/data_format_inference.md#data-format-for-inference). 
The instructions for preparing the dataset are described [here](https://github.com/MIC-DKFZ/nnUNet/tree/nnunetv1#dataset-conversion).
Remember that when preparing the dataset, the first image "0000" should be QSM, and the second image "0001" should be T1 or FLAIR.
To run the segmentation, the following command could be used 
```bash
nnUNet_predict -i </path/to/test_images> -o </path/to/output_folder> -tr nnUNetTrainerV2 -ctr nnUNetTrainerV2CascadeFullRes -m 3d_fullres -p nnUNetPlansv2.1 -t <task-id>
```
The task-id could be the same as the trained models, e.g. "Task601_QSM_T1".

# Repository status 
Please note that this repository is currently under development and is not yet complete. 
We are actively working to enhance the documentation and include related codes. 
We appreciate your patience and encourage you to check back often for the latest advancements. 
If you have any suggestions or would like to contribute to the project, please don't hesitate to let us know.
