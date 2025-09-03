# Work in progress.  La repo sarà completa prima della scadenza all'iscrizione dell'appello.

# Exercise 1.1 and 1.2
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

# Exercise 1.3
The goal of this exercise is to repeat the analysis from Exercise 1.2, this time using Convolutional Neural Networks trained on CIFAR-10. As expected, we observe improvements when residual connections are used.
<p align="center">
 <img width="650"  alt="cnn" src="https://github.com/user-attachments/assets/6dd5cc4a-a69f-4b1e-a061-99520c5ac3e0" />
</p>
<p align="center">
  <sub><em>
    Accuracy curves during training. The numbers next to each model name indicate the number of residual blocks (with or without skip connections enabled). Models with residual connections achieve consistently higher accuracy than the plain versions.
  </em></sub>
</p>

# Exercise 2.3  
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
<img width="850" alt="imagenette_cam_6images" src="https://github.com/user-attachments/assets/75fb30ff-de0c-4856-b595-dc0a002c43e8" />
</p>
<p align="center">
