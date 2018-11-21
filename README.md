[//]: # (Image References)

[image1]: ./images/sample_dog_output.png "Sample Output"
[image2]: images/Curly-coated_retriever_03896.jpg "Retriever"

# Convolutional Neural Network Dog Classifier

## Overview

Given an image of a dog, this [notebook](dog_app.ipynb) will identify an estimate of the canine’s breed.  If supplied an image of a human, the code will identify the resembling dog breed.  

![Sample Output][image1]

## Details

### Training Data

Training data consists of over 8000 dog images tagged with their breed's. The imaged are split into training, test and validation sets.

The data contains instances of minimal inter-class variation, such as retrievers and spaniels.

| Retriever | Spaniel |
| ---- | ---- |
| <img src="https://github.com/Tomesco/dog-breed-classifier/blob/master/images/Curly-coated_retriever_03896.jpg?raw=true" height=200px> | <img src="https://github.com/Tomesco/dog-breed-classifier/blob/master/images/American_water_spaniel_00648.jpg?raw=true" height=200px> |

There are also cases of high intra-class variation, such as within Labradors.

| Yellow Labrador | Chocolate Labrador | Black Labrador |
| --- | --- | --- |
| <img src="https://github.com/Tomesco/dog-breed-classifier/blob/master/images/Labrador_retriever_06457.jpg?raw=true" height=150px> | <img src="https://github.com/Tomesco/dog-breed-classifier/blob/master/images/Labrador_retriever_06455.jpg?raw=true" height=150px> | <img src="https://github.com/Tomesco/dog-breed-classifier/blob/master/images/Labrador_retriever_06449.jpg?raw=true" height=150px> |

### Import Human Face Detector

OpenCV's [human face detector](https://docs.opencv.org/trunk/d7/d8b/tutorial_py_face_detection.html) using Haar Cascades is used here.

### Import Dog Detector

The [ResNet-50](http://ethereon.github.io/netscope/#/gist/db945b393d40bfa26006) model is used to identify images containing dogs.

The images are preprocessed according to ResNet-50's specifications (normalized and resized).

### Train Dog Classifier

Transfer learning is used to create a CNN using [Xception](https://towardsdatascience.com/review-xception-with-depthwise-separable-convolution-better-than-inception-v3-image-dc967dd42568) bottleneck features.

A 500 paramter layer is added to focus on the current dog image dataset, followed by a 133 parameter fully-connected layer.

Training was performed on an EC2 GPU instance.