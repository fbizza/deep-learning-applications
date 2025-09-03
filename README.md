# Work in progress.  La repo sarà completa prima della scadenza all'iscrizione dell'appello.

# Exercise 1.1
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



