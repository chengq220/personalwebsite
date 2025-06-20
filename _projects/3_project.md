---
layout: page
title: Medical Segmentation
description: Research project on medical segmenetation using U-Net
img: assets/img/project_medical_backup.png
# redirect: https://github.com/chengq220/Hybrid_UNet
importance: 3
category: research
related_publications: false
---

Convolutional Neural Networks (CNNs) have been extensively used in critical sectors such as healthcare for more effciient diagnosis of diseases like tumors in medical imaging. However, structures in medical images are often complicated and comes in various shapes and forms. These complexities have contributed to the difficulty for tasks like binary segmentation of tumors (foreground) from irrevlant pixels (background). Issues such as boundary blurring between the background and foreground have been a limiting factor in more reliance on such technologies. 

One of the architectures currently used in fields such as medical imaging is the U-Net, which is a encoder decoder network desgined specifically for segmentation tasks. 

<div class="row justify-content-sm-center ">
    <div class="align-self-center w-50">
        {% include figure.liquid loading="eager" path="assets/img/unet.png" title="U-Net Architecture" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption text-center">
    The architecture of a U-Net
</div>

Each of the layer in the U-Net are composed of two main operation, namely convolution and max-pooling. In the context of the U-Net, the convolution layer contains a learnable parameter represented by the rectangular kernel to extract patterns from the feature map inputted into each layer. The max-pooling down sample the feature map by selecting most signficant value across spatial and channel dimension. Together, the stacking of these layers gives U-Net it's strong reprsentative learning ability for medical images. 

However, the operations are all confined by its geometry, specifically it only operates in a retangular manner (i.e. convolution kernel and pooling). This project seeks to explore the use of graph-based methods such as meshes to tackle the binary segmenetation task for medical images. Instead, the image is reprsented by a triangular mesh with each pixel representing a node and each node is only connected to its immediate neighbors and lower left node. 

<div class="row justify-content-sm-center ">
    <div class="align-self-center w-25">
        {% include figure.liquid loading="eager" path="assets/img/triangular.png" title="Triangular Representation" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption text-center">
    Figure 2. The graph representation of images
</div>

With this representation, the traditional convolution and pooling will not be compatible. For the convolution, recent results in spline convolution made it an ideal choice as the learnable parameter reprsenting B-Splines (shown in Figure 3). Inspired by MeshCNN, we adapted their mesh pooling scheme, which merges 2 faces into 2 edges without violating the mesh property, to replace the max pooling (shown in Figure 4).

<div class="row justify-content-sm-center ">
    <div class="align-self-center w-25">
        {% include figure.liquid loading="eager" path="assets/img/Spline_basis.png" title="Spline" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption text-center">
    Figure 3. (Taken from SplineCNN Paper) Spline basis function for convolution
</div>

<div class="row justify-content-sm-center ">
    <div class="align-self-center w-25">
        {% include figure.liquid loading="eager" path="assets/img/mesh_pooling.png" title="Mesh Pooling" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption text-center">
    Figure 4. (Taken from MeshCNN Paper) Mesh pooling and unpooling operation
</div>

Experimentation on this implementation showed that the Hybrid U-Net that we proposed is almost on par with the baseline. However, due to the complexity of meshes, the efficiency of the implementation (specifically mesh pooling) needed to be reinterpreted and overhauled as it takes much longer to train than the traditional U-Net implementaiton which uses operations that are vectorized. 

You can check out the implementation at

    ---
    https://github.com/chengq220/Hybrid_UNet
    ---
