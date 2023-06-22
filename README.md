# Fast Symmetric Diffeomorphic Image Registration with Convolutional Neural Networks

This is the official Pytorch implementation of "Fast Symmetric Diffeomorphic Image Registration with Convolutional Neural Networks" (CVPR 2020), written by Tony C. W. Mok and Albert C. S. Chung.

\*\* Please also check out our new deep learning-based image registration framework ([LapIRN - MICCAI2020](https://arxiv.org/abs/2006.16148 "eprint arXiv:2006.16148")) at https://github.com/cwmok/LapIRN, which achieved promising registration performance in large deformation settings. \*\*

## Prerequisites
- `Python 3.5.2+`
- `Pytorch 1.3.0`
- `NumPy`
- `NiBabel`

This code has been tested with `Pytorch` and GTX1080TI GPU.

## Inference
```
python Test_SYMNet.py
```

## Training
If you want to train a new model using your own dataset, please define your own data generator for `train_SYMNet.py` and perform the following script.
```
python train_sym_onepass.py
```

## (Example) Training on the preprocessed OASIS dataset
If you want to train on the preprocessed OASIS dataset in https://github.com/adalca/medical-datasets/blob/master/neurite-oasis.md. We have an example showing how to train on this dataset.
1. Download the preprocessed OASIS dataset, unzip it and put it in "Data/OASIS".
2. To train a new SyMNet, `python Train_sym_neurite_oasis.py` will create a SyMNet model trained on the first 255 cases in the dataset.
3. To test the model, `python Test_SYMNet_neurite_oasis.py --modelpath {{pretrained_model_path}} --fixed ../Data/image_A_full_size.nii.gz --moving ../Data/image_B_full_size.nii.gz` will load the assigned model and register the image "image_A_full_size.nii.gz" and "image_B_full_size.nii.gz".

A pretrained model and its log file are available in "Model/SYMNet_neurite_oasis_smo30_update_80000.pth" and "Log/SYMNet_neurite_oasis_update.txt", respectively.

## Publication
If you find this repository useful, please cite:

- **Fast Symmetric Diffeomorphic Image Registration with Convolutional Neural Networks**  
[Tony C. W. Mok](https://cwmok.github.io/ "Tony C. W. Mok"), Albert C. S. Chung  
CVPR 2020. [eprint arXiv:2003.09514](https://arxiv.org/abs/2003.09514 "eprint arXiv:2003.09514")

## Notes on this repository
We found that estimating the time 1 solution instead of 0.5 solution tends to produce a smoother result in our later experiments. If you want to switch back to 0.5 solution, please replace the "self.time_step" with "self.time_step-1" at line 165 in `Models.py` and train a new model from scratch.

## Acknowledgment
Some codes in this repository are modified from [IC-Net](https://github.com/zhangjun001/ICNet) and [VoxelMorph](https://github.com/voxelmorph/voxelmorph).

###### Keywords
Keywords: Diffeomorphic Image Registration, convolutional neural networks, alignment, Symmetric Image Registration
