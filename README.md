# Segmentation of midbrain structures using nnU-Net and multi-sequence MRI data

This repository contains trained deep learning networks for the segmentation of key midbrain nuclei, the subthalamic nucleus (STN), substantia nigra (SN), and red nucleus (RN). The networks are based on the [nnU-Net](https://github.com/MIC-DKFZ/nnUNet/tree/nnunetv1) framework. 
The networks are trained using multi-sequence MRI data, specifically, T1-weighted, T2-FLAIR, and Quantitative Susceptibility Mapping (QSM) images. 
The networks are trained on 40 brain images, where the nuclei were manually traced on for each nucleus on QSM images.

For more information, please read [this paper](https://doi.org/10.1162/imag_a_00304):
Farshad Falahati, Jonatan Gustavsson, Grégoria Kalpouzos; Automated segmentation of midbrain nuclei using deep learning and multisequence MRI: A longitudinal study on iron accumulation with age. Imaging Neuroscience 2024; 2 1–20. doi: https://doi.org/10.1162/imag_a_00304

## Trained networks
The trained networks could be downloaded from this [link](https://1drv.ms/u/s!Ai108NIExicshy-jF9FlZvhL515W?e=2tEFvR).
There are two trained networks available: the first is trained using QSM and FLAIR images, while the second is trained with QSM and T1 images. 
Please note that these networks have been validated only on a dataset of MRI data collected from a single MR scanner, using consistent imaging parameters. 
Their performance has not been validated on datasets collected with other scanners. 
Therefore, we recommend using the networks with caution. 
They may serve optimally as initial models for transfer learning or for further fine-tuning.

## Using the networks 
In order to use the networks, [nnU-Net-v1](https://github.com/MIC-DKFZ/nnUNet/tree/nnunetv1) library should be installed. 
The installation process is described [here](https://github.com/MIC-DKFZ/nnUNet/tree/nnunetv1#installation). 
nnU-Net is based on [PyTorch](https://pytorch.org/) and PyTorch should be installed before installing nnU-Net. 
The instructions for installing PyTorch are available [here](https://pytorch.org/get-started/locally/). 

Following a successful installation of PyTorch and the nnU-Net library, the dataset should be prepared. 
nnU-Net expects datasets in [specific format](https://github.com/MIC-DKFZ/nnUNet/blob/nnunetv1/documentation/data_format_inference.md#data-format-for-inference). 
The instructions for preparing the dataset are described [here](https://github.com/MIC-DKFZ/nnUNet/tree/nnunetv1#dataset-conversion).
The trained model in this project are named Task600_QSM_FLAIR and Task601_QSM_T1 and the data could be structured as follow: 

    nnUNet_raw_data_base/nnUNet_raw_data/
        ├── Task600_QSM_FLAIR
        |       ├── dataset.json
        |       └── imagesTs
        |               ├── Sub001_0000.nii.gz  (QSM image for subject 1)
        |               ├── Sub001_0001.nii.gz  (FLAIR image for subject 1)
        |               ├── Sub002_0000.nii.gz  (QSM image for subject 2)
        |               ├── Sub002_0001.nii.gz  (FLAIR image for subject 2)
        |               ├── ...
        |
        |
        └── Task601_QSM_T1
                ├── dataset.json
                └── imagesTs
                        ├── Sub001_0000.nii.gz  (QSM image for subject 1)
                        ├── Sub001_0001.nii.gz  (T1 image for subject 1)
                        ├── Sub002_0000.nii.gz  (QSM image for subject 2)
                        ├── Sub002_0001.nii.gz  (T1 image for subject 2)
                        ├── ...


Note that the first image "0000" should be QSM, and the second image "0001" should be T1 or FLAIR. 
Also, QSM and FLAIR/T1 images should be in the same space. We registered both QSM and FLAIR images to T1 space. 


To run the segmentation, the following command could be used 
```bash
nnUNet_predict -i </path/to/test_images> -o </path/to/output_folder> -tr nnUNetTrainerV2 -ctr nnUNetTrainerV2CascadeFullRes -m 3d_fullres -p nnUNetPlansv2.1 -t <task-id>
```
The task-id could be the same as the trained models, e.g. "Task601_QSM_T1".

## Repository status

**Please note that this repository is currently under development and is not yet complete. 
We are working to enhance the documentation and include related codes. 
We appreciate your patience and encourage you to check back often for the latest advancements. 
If you have any suggestions or would like to contribute to the project, please don't hesitate to contact us.**

