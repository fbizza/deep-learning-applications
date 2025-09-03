# deep-learning-applications
This repository contains the code developed to solve the exercises for the Deep Learning Applications course (2024/25). The results are presented below
<h1 align="center">Laboratory 1</h1>

## Exercise 1.1 and 1.2
The goal of this exercise is to demonstrate the importance of **residual connections**. We do this by evaluating simple MLPs and showing that deeper networks with residual connections are easier to train compared to networks of the same depth without residual connections.  We compare MLPs with a width of 16 and varying depths on the MNIST dataset.
 

<p align="center">
Note: For this first experiment, each residual block contains 1 layer
</p>

<div align="center">

| Depth | Accuracy (MLP) | Accuracy (ResidualMLP) |
|:-----:|:--------------:|:--------------------:|
| 2     | 0.93           | **0.94**             |
| 8     | 0.88           | **0.95**             |
| 32    | 0.11           | **0.95**             |
| 64    | 0.11           | **0.35**             |

</div>

Notice the poor performance of the last Residual MLP (depth 64). This was improved by increasing the number of layers per residual block from 1 to 2:

<div align="center">

| Depth | Accuracy (MLP) | Accuracy (ResidualMLP, 2 layers/block) |
|:-----:|:--------------:|:--------------------------------------:|
| 2     | 0.93           | **0.93**                               |
| 8     | 0.88           | **0.95**                               |
| 32    | 0.11           | **0.96**                               |
| 64    | 0.11           | **0.96**                               |

</div>


The figure below shows the magnitude of gradients as they propagate through the network, comparing a standard MLP and a MLP with residual blocks. The zig-zag pattern in the graph occurs because gradients for **biases and weights were not separated** in this visualization. Despite this, it is clear that residual connections help preventing vanishing gradients.
<p align="center">
<img width="600"alt="gradients" src="https://github.com/user-attachments/assets/8302cfb4-6fa2-46a0-80fe-98e9e654cc69" />
</p>

## Exercise 1.3
The goal of this exercise is to repeat the analysis from Exercise 1.2, this time using Convolutional Neural Networks trained on CIFAR-10. As expected, we observe improvements when residual connections are used.
<p align="center">
 <img width="650"  alt="cnn" src="https://github.com/user-attachments/assets/6dd5cc4a-a69f-4b1e-a061-99520c5ac3e0" />
</p>
<p align="center">
  <sub><em>
    Accuracy curves during training. The numbers next to each model name indicate the number of residual blocks (with or without skip connections enabled). Models with residual connections achieve consistently higher accuracy than the plain versions.
  </em></sub>
</p>

## Exercise 2.3  
The goal of this exercise is to explain the predictions of a CNN by visualizing **Class Activation Maps (CAMs)**. We use the CNN trained in Exercise 1.3 and extend it with CAM to highlight which regions of the input image contribute most to the model’s classification decision. 
<p align="center">
<img width="1000" alt="cifar10_cam_6images" src="https://github.com/user-attachments/assets/52d48dfd-bbd3-45d7-8690-6d26b250def2" />
</p>
<p align="center">
  <sub><em>
CAMs showing which image regions the trained CNN focuses on (CIFAR-10).
  </em></sub>
</p>

We also apply CAM to a pre-trained ResNet-18 on images from the Imagenette dataset:

<p align="center">
<img width="1000" alt="imagenette_cam_6images" src="https://github.com/user-attachments/assets/75fb30ff-de0c-4856-b595-dc0a002c43e8" />
</p>
<p align="center">


<h1 align="center">Laboratory 4</h1>

## Exercise 1.1
In this exercise, we build a simple **Out-of-Distribution (OOD) detection pipeline**. The in distribution (ID) used dataset is CIFAR-10, while the OOD datasets are a subset of CIFAR-100 (with classes not present in CIFAR-10) and randomly generated FakeData. For brevity only results using CIFAR-100 are discussed.

The maximum softmax probability is used for representing how OOD a test sample is. It is produced by a custom small CNN and a pretrained ResNet-20 model.
<div align="center">
 
| Custom CNN | ResNet |
|--------------------|---------------|
| <div align="center"> <img width="300" src="https://github.com/user-attachments/assets/9a2b83fa-3637-4608-bfd7-0504e6b5af4b" /> </div> | <div align="center"> <img width="300" alt="histogram" src="https://github.com/user-attachments/assets/136e60d5-5e2b-43ba-9f94-22daeab0c7bf" /> </div> |
| <div align="center"> <img width="300" alt="auc" src="https://github.com/user-attachments/assets/fb2859fa-ce9d-4092-8073-2f47b9250f5e" /> </div> | <div align="center"> <img width="300" alt="auc" src="https://github.com/user-attachments/assets/9f13616b-4b9d-4c59-8fac-2b4b122deaff" /> </div> |
| <div align="center"> <img width="300" alt="ap" src="https://github.com/user-attachments/assets/23978d0a-7333-416c-8f4a-2b3acf51eb22" /> </div> | <div align="center"> <img width="300" alt="ap" src="https://github.com/user-attachments/assets/31c0fa1f-41d7-4c8e-9d9e-f81e7432e2fc" />

</div>





TODO: add note about use of genAI
