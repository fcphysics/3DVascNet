# 3D Vessel Segmentation
Semi-Supervised 3D Vessel Segmentation in Microscopy Images of Mouse Retinas 

This repository contains the Python implementation of a 3D cycleGAN model to segment blood vessels in 3D microscopy images of mouse retinas.

## Dataset

Our dataset contains 3D microscopy images of mouse retinas and the corresponding 2D segmentation masks (annotated manually based on the maximum intensity projection (MIP) images of the 3D microscopy images). Moreover, we have the 3D segmentation masks obtained based on the 2D segmentation masks using [PolNet](https://github.com/mobernabeu/polnet).


## Pre-Processing

To apply the pre-processing vessel enhancement method run the file [percentile.py](https://github.com/HemaxiN/3DVesselSegmentation/blob/main/preprocessing/percentile.py). Moreover, the code to convert the ```.stl``` objects (3D segmentation masks obtained with [PolNet](https://github.com/mobernabeu/polnet)) into 3D ```.tif``` files is provided in the jupyter notebook [STL2Voxel.ipynb](https://github.com/HemaxiN/3DVesselSegmentation/blob/main/preprocessing/STL2Voxel.ipynb).

## Training on Your Own Dataset


To create the training patches (images and masks) use the files [create_patches_images.py](https://github.com/HemaxiN/3DVesselSegmentation/blob/main/preprocessing/create_patches_images.py) and [create_patches_masks.py](https://github.com/HemaxiN/3DVesselSegmentation/blob/main/preprocessing/create_patches_masks.py), respectively. Furthermore, patches representing the background can be created running the file [create_background_patches.py](https://github.com/HemaxiN/3DVesselSegmentation/blob/main/preprocessing/create_background_patches.py).

Run the file [train_main.py](https://github.com/HemaxiN/3DVesselSegmentation/blob/main/train_main.py) after changing the parameters defined in this file.
The `train_dir` contains the following tree structure:

```
train_dir
   ├── images  0.tif, 1.tif, ..., N.tif (patches of microscopy images of vessels  (Z_slices, X_dim, Y_dim, Channels))
   └── masks   0.tif, 1.tif, ..., N.tif (patches of segmentation masks of vessels  (Z_slices, X_dim, Y_dim, Channels))
```


## Prediction

To test the trained model on new images specify the directories in file [predict_main.py](https://github.com/HemaxiN/3DVesselSegmentation/blob/main/predict_main.py) and run it.

## Post-Processing and Evaluation

Post-Processing methods can be applied to the predicted segmentation masks using the files [post_proc_main.py](https://github.com/HemaxiN/3DVesselSegmentation/blob/main/post_proc_main.py) and [erosion.py](https://github.com/HemaxiN/3DVesselSegmentation/blob/main/erosion.py); and the performance of the model can be evaluated using [eval_main.py](https://github.com/HemaxiN/3DVesselSegmentation/blob/main/eval_main.py). 

## Requirements

Python 3.5.2, Keras 2.2.4 and other packages listed in [requirements.txt](https://github.com/HemaxiN/3DVesselSegmentation/blob/main/utils/requirements.txt).


## Acknowledgements

* Code based on the [2D implementation of the cycleGAN](https://machinelearningmastery.com/cyclegan-tutorial-with-keras/);
* [STL2Voxel](https://github.com/cpederkoff/stl-to-voxel).


create_patches_images.py
create_patches_masks.py

create_background_patches.py (optional)

train_main.py

predict_main.py

post_proc_main.py

erosion.py (optional)

eval_main.py
