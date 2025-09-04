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

## Exercise 1
In this exercise, we build a simple **Out-of-Distribution (OOD) detection pipeline**. The dataset used for in distribution (ID) examples is CIFAR-10, while the OOD datasets are a subset of CIFAR-100 (with classes not present in CIFAR-10) and randomly generated FakeData. For brevity only results using CIFAR-100 are discussed.

The maximum softmax probability is used for representing how OOD a test sample is. This probability is produced by a custom small CNN and a pretrained ResNet-20 model that i compare in the following table:
<div align="center">
 
|  | Custom CNN | ResNet |
|-----------|---------|---------------|
| **Histogram** |<div align="center"> <img width="300" src="https://github.com/user-attachments/assets/9a2b83fa-3637-4608-bfd7-0504e6b5af4b" /> </div> | <div align="center"> <img width="300" alt="histogram" src="https://github.com/user-attachments/assets/136e60d5-5e2b-43ba-9f94-22daeab0c7bf" /> </div> |
| **ROC curve**| <div align="center"> <img width="300" alt="auc" src="https://github.com/user-attachments/assets/fb2859fa-ce9d-4092-8073-2f47b9250f5e" /> </div> | <div align="center"> <img width="300" alt="auc" src="https://github.com/user-attachments/assets/9f13616b-4b9d-4c59-8fac-2b4b122deaff" /> </div> |
| **PR curve** | <div align="center"> <img width="300" alt="ap" src="https://github.com/user-attachments/assets/23978d0a-7333-416c-8f4a-2b3acf51eb22" /> </div> | <div align="center"> <img width="300" alt="ap" src="https://github.com/user-attachments/assets/31c0fa1f-41d7-4c8e-9d9e-f81e7432e2fc" />

</div>

As shown in the plots, the ResNet performs better. This is expected since it also achieves higher classification accuracy on CIFAR-10 (81%) compared to the smaller custom CNN (64%).

## Exercise 2.1

In this exercise the **FGSM** method is used to generate adversarial examples. The model used  is the custom CNN introduced in the previous exercise.
Here are shown some examples of adversarial attacks generated with an *epsilon* = 1/255:
<div align="center">
<img width="700" alt="output1" src="https://github.com/user-attachments/assets/b61235e5-a3d7-419f-8c4a-d0bbdee131c9" />
</div>

<div align="center">
<img width="700" alt="output2" src="https://github.com/user-attachments/assets/cf5e0587-9e5c-4080-9692-8c81e84e2c39" />
</div>


I used 3 metrics in order to evaluate how dependent on *epsilon* the generated adversarial images are:

- Attack success rate
- Average iterations to success
- Average confidence drop
  
(All the attacks have a fixed *max_n_iterations = 10*)

<img width="900"  alt="quantitative_eval" src="https://github.com/user-attachments/assets/486d67e3-cdfd-4f95-bb53-0a4c2c4a3a4f" />

As expected bigger *epsilons* produce more powerful (but also more noticeable) attacks .

## Exercise 2.2

In this exercise FGSM adversarial samples are used to augment the training dataset used to train the the OOD detector model. 
The way i implemented this augmented training is by using a weighted loss function in the training loop. For each batch, I compute the loss on both the original (clean) inputs and the adversarially perturbed inputs, then combine them to form a single loss. The weights of the loss components are hyperparameters. 

For an equally weighted loss, **loss = 0.5 * clean_loss + 0.5 * adv_loss**, there is a slight improvement of about 2% in both the ROC and PR curves. 

<div align="center">
<img width="250"  alt="augmented_1" src="https://github.com/user-attachments/assets/beaf16b9-bc38-42b7-b63f-5e23ec30818b" />
<img width="250"  alt="augmented_2" src="https://github.com/user-attachments/assets/65fa44b5-aad9-4106-a664-ca3997f6ce05" />
 
   <sub><em>
65% and 87% vs 63% and 85% of (non augmented training) from exercise 1
  </em></sub>
</div>

For an unbalanced loss, **loss = 0.2 * clean_loss + 0.8 * adv_loss**, the performance slightly degrades. This suggests that the hyperparameter weights of the components of the loss might be tricky to tune.
<div align="center">
<img width="250" alt="output_4" src="https://github.com/user-attachments/assets/22d55e3c-2e8d-4af0-9614-9da5bbf3764a" />
<img width="250" alt="output_5" src="https://github.com/user-attachments/assets/c688ce89-ccba-43e4-aaca-eb6c0c964c0b" />
</div>

## Exercise 3.3
The goal of this exercise was to generate **targeted** attacks by creating adversarial samples that *imitate* samples from a specific class. Here is a qualitative evaluation of 2 of them, where the target class was "dog":

<div align="center">
 <img width="700" alt="output_1" src="https://github.com/user-attachments/assets/7066f59b-ef49-4199-acca-5e0f63201f1f" />
</div>

<div align="center">
 <img width="700" alt="output_2" src="https://github.com/user-attachments/assets/9f612264-b0fc-4330-b083-09d57f729c59" />
</div>

For a quantitative evaluation i compared the targeted and non targeted attacks using the 3 metrics introduced in exercise 2.1. The model used to generate images is the same (custom CNN trained in exercise 2.2). For both types of attacks *epsilon = 1/255* and *max_n_iterations = 10*.

<div align="center">
<img width="800"alt="comparison" src="https://github.com/user-attachments/assets/0d09fe44-2035-40a6-aa5c-015481608e24" />
 
 <sub><em>
As expected, the average confidence drop is larger and the average number of iterations to success is lower for untargeted attacks compared to targeted ones. This behavior arises because untargeted attacks only need to push the sample outside the decision region of the true class, which is a simpler optimization problem. What is surprising is that the success rate is slightly higher for targeted attacks. This might be the effect of the augmented training done during exercise 2.2, where the augmentation was based on untargeted attacks.
  </em></sub>
</div>


TODO: add note about use of genAI
