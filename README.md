[readme.md](https://github.com/user-attachments/files/30063859/readme.md)
# Astronomical_Figures_Classification
This is my final NVIDIA project.

Astronomical_Figures_Classification

Using Kaggles Astronomy Image Classification Dataset, this project can classify constellations, cosmos space, galaxies, nebula, planets, and stars.

<img width="3508" height="2112" alt="constellation1" src="https://github.com/user-attachments/assets/e70a0cef-1ad9-49f2-b42c-16d0660632a0" />
This is an example of the model classifiying this image as constellation with 48.36% certainty.

## The Algorithm
I used InageNet for the classification.

## Running this project:

#### Downloads dataset
#!/bin/bash
curl -L -o ~/Downloads/space-images-category.zip\
  https://www.kaggle.com/api/v1/datasets/download/abhikalpsrivastava15/space-images-category


#### Goes to data in classification in training in python in jetson inference
cd jetson-inference/python/training/classification/data

#### Unzips dataset
unzip ~/Downloads/space-images-category.zip -d space_images

#### Goes to jetson inference
cd ~/jetson-inference

#### Goes to docker
./docker/run.sh

#### Goes to classification in training in python
cd python/training/classification

#### Trains the model
python3 train.py --model-dir=models/space_images data/space_images

#### Exports as ONNX 
python3 onnx_export.py --model-dir=models/space_images

#### Sets the NET and DATASET variables
NET=models/space_images
DATASET=data/space_images

#### Tests an image
imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/constellation/27.jpg constellation1.jpg

## Video
https://drive.google.com/file/d/1BC3hlPdlXRjIQP_fwGocJ_7yXm45r7LL/view?usp=sharing
