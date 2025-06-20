---
layout: page
title: Emotion Detection
description: Research project on emotion detection using deep learning techniques
img: assets/img/project_emotion.jpg
importance: 4
category: research
related_publications: false
---

Deep learning techniques have emerged as a transformative tool in addressing complexity for emotion detection and classification. With their ability to learn intricate patterns from large datasets, these methods enable the detection of subtle cues in facial expressions, voice intonations, and other physiological signals. This research project aims to leverage the power of deep learning to improve emotion detection systems, making them more accurate, robust, and adaptable to diverse real-world scenarios. The findings of this study could not only advance the field of affective computing but also contribute to the development of empathetic AI technologies, enhancing human-machine interaction and fostering inclusivity in applications like education, healthcare, and assistive technologies.

Inspired by the COVID-19 situation where people were usually wearing masks outside, this project investigate the extent to which removing key features from iconic facial images will affect the performance. Though the preliminary result showed decreased perforamnce in general, but this trend was not observed for all the emotion classes. This raised the idea that potentially isolating key facial features during training may help deep learning classifier generalize better for emotion detection task. Building on this hypothesis, we proposed a new training scheme for training existing deep learning classifiers. Fer2013, a facial emotion dataset containing 7 classes, was used for the project. However, some of the issues with this dataset are the imbalance of samples from each classes, making it less ideal and incorrect labeling of samples. 

<div class="row justify-content-sm-center ">
    <div class="align-self-center w-50">
        {% include figure.liquid loading="eager" path="assets/img/datadistribution.png" title="Fer2013 Distribution" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption text-center">
    Figure 1. Distribution of the Fer2013 dataset.
</div>


The proposed scheme clusters the pixels into n different classes base on its pixel location and the pixel attention. During training, each of these classes are removed. This method was tested on several popular classifier such as ResNet, CNN, dual path network, etc using Fer2013 dataset. The proposed method tackle this challenge indirectly by increasing the samples of images available for training which also help in enhancing performance. 

<div class="row justify-content-sm-center ">
    <div class="align-self-center w-50">
        {% include figure.liquid loading="eager" path="assets/img/new_scheme.png" title="Propose scheme" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption text-center">
    Figure 2. Proposed Method
</div>

For the proposed method, one hyperparameter that need to be set is the number of clusters for the k-clustering algorithm. After some testing, the number of classes for clustering was determined to be optimal at n = 3. 

<div class="row justify-content-sm-center">
    <div class="col-sm-5 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/clusterelbow.png" title="Cluster Exp" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-7 mt-3 mt-md-0 d-flex align-items-center">
        {% include figure.liquid path="assets/img/masked.png" title="Masked Image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
     Figure 3. (Left) The optimal number of clusters. (Right) Facial image after removal of a cluster 
</div>

After integrating the proposed methodology into existing models, experimentat was conducted and the following tables showed the results. 

<div class="row justify-content-sm-center">
    <div class="col-sm-5 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/baseline.png" title="Baseline" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-5 mt-3 mt-md-0 d-flex align-items-center">
        {% include figure.liquid path="assets/img/perturb.png" title="Perturb" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
     Figure 4. Performance comparison of baseline and proposed method
</div>

In general, the proposed method resulted in increase in perforamnce. From figure 5, it can be obnserved that for some emotions like fear, the classifier trained by the proposed method was able to focus more on the mouth which is the distinguishing factor from similiar emotions like sad. It's likely that the additional training data available to the model also contributed to this performance gain. 

<div class="row justify-content-sm-center ">
    <div class="align-self-center w-50">
        {% include figure.liquid loading="eager" path="assets/img/result_salient.png" title="Salient Map" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption text-center">
    Figure 5. Saliency map for emtions produced by baseline model (top) and model trained using proposed method (bottom)
</div>


You can check out the code and paper @

    ---
    Paper: https://arxiv.org/abs/2411.00824
    Code : https://github.com/chengq220/EmotionDetection
    ---