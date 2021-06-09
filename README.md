# Plant Pathology 2021 - FGVC8

This repository contains the code for the solution I submitted for the Kaggle [**Plant Pathology 2021 challenge**](https://www.kaggle.com/c/plant-pathology-2021-fgvc8), which took place from March 15 2021 to May 27 2021. This competition was part of the Fine-Grained Visual Categorization [FGVC8](https://sites.google.com/view/fgvc8) workshop at the Computer Vision and Pattern Recognition Conference [CVPR 2021](http://cvpr2021.thecvf.com/).

A corresponding article can be found on my website [**here**](https://antonindurieux.github.io/portfolio/1_Kaggle_Plant_Pathology_2021_competition/).

This competition was a good opportunity to explore some technical topics related to Convolutional Neural Networks and computer vision such as :
- How to implement a CNN taking advantage of [TPUs](https://www.kaggle.com/docs/tpu) to speed up the computing steps ;
- How to build an efficient TensorFlow input pipeline with the [`tf.data` API](https://www.tensorflow.org/guide/data) ;
- What loss could be suitable for optimizing the F1-score ;
- What is a Vision Transformer and how to use it ?

My solution ranked **11th out of 626 teams** on the public leaderboard, and **36th** on the private leaderboard (**top 6%**).

## Task

As stated on the [competition description page](https://www.kaggle.com/c/plant-pathology-2021-fgvc8/overview/description) : 

> "Apples are one of the most important temperate fruit crops in the world. Foliar (leaf) diseases pose a major threat to the overall productivity and quality of apple orchards. The current process for disease diagnosis in apple orchards is based on manual scouting by humans, which is time-consuming and expensive."

The task of this challenge was thus to develop a machine learning-based model to **identify diseases on images of apple tree leaves**. 

Each leaf could be healthy, or present a combination of various diseases. As each image could potentially be associated with several labels (in case of multiple diseases), this was a **multi-label classification** task.

## Data

For the purpose of the competition, a dataset of **18632** labeled apple tree leaf images was provided. 

The test set used to evaluate the participant submissions was constituted of roughly **2700** images. 

The pictures were provided in jpeg format of relatively high resolution, lots of them being 2676 x 4000 pixels, but the resolution and aspect ratio could somewhat vary for some images.

![](/assets/plant_pathology_examples.png)

## Performance metric

The evaluation metric for this competition was the **Mean F1-score**. 

## General approach

My best score was reached by averaging the output of 3 different models :
- a **ResNet50**, 
- an **EfficientNetB7**, 
- and a [**Vision Transformer**](https://ai.googleblog.com/2020/12/transformers-for-image-recognition-at.html) model.

On top of the training process optimizations, significant results improvements were brought by :
- Suitable image augmentation,
- Handling the cases were no label has been predicted by the model (probability of every label inferior to the chosen threshold),
- Test Time Augmentation (TTA) (see [this article](https://towardsdatascience.com/test-time-augmentation-tta-and-how-to-perform-it-with-keras-4ac19b67fb4d) for a brief explanation on how it works).

![](/assets/plant_pathology_diagram.png)

## Usage

4 Notebooks are available in this repository :
- [**1_plant-pathology-2021-fgvc8-resnet50-training.ipynb**](https://github.com/antonindurieux/Plant_Pathology_2021-FGVC8_Kaggle_challenge/blob/master/1_plant-pathology-2021-fgvc8-resnet50-training.ipynb) explains the training of the ResNet50 model in details ;
- [**2_plant-pathology-2021-fgvc8-efficientnetB7-training.ipynb**](https://github.com/antonindurieux/Plant_Pathology_2021-FGVC8_Kaggle_challenge/blob/master/2_plant-pathology-2021-fgvc8-effnetb7-training.ipynb) contains the code of the EfficientNetB7 model training with only brief explanations as the steps are much the same as for the ResNet50 model ;
- [**3_plant-pathology-2021-fgvc8-vit-training.ipynb**](https://github.com/antonindurieux/Plant_Pathology_2021-FGVC8_Kaggle_challenge/blob/master/3_plant-pathology-2021-fgvc8-vit-training.ipynb) contains the code of the Vision Transformer model training with only brief explainations as the steps are much the same as for the previous two model ;
- [**4_plant-pathology-2021-fgvc8-inference.ipynb**](https://github.com/antonindurieux/Plant_Pathology_2021-FGVC8_Kaggle_challenge/blob/master/4_plant-pathology-2021-fgvc8-inference.ipynb) contains the code of the inference process.
