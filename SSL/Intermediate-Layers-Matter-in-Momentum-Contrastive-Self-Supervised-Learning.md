# Intermediate Layers Matter in Momentum Contrastive Self Supervised Learning

```
Authors: Akash Kaku, Narges Razavian, Sahana Upadhya
Authors' affliation: New York University
Fields: AI, CV, self-supervised learning
Priority: high
Read: Yes
Read Date: February 13, 2022
Venue: NeurIPS
Year: 2021
code: https://github.com/aakashrkaku/intermdiate_layer_matter_ssl
```
Links: [[paper](https://arxiv.org/abs/2110.14805)]

## Hightlight

self-supervised learning, MoCo, Barlow Twins, medical image

## Prerequisite

- Barlow Twins: [[paper](https://arxiv.org/abs/2103.03230)] [[summary](https://www.notion.so/Barlow-Twins-Self-Supervised-Learning-via-Redundancy-Reduction-e020a96ed95844d4bbfd7768c0113b10)]
- MoCo: [[paper](https://arxiv.org/abs/1911.05722)]

## What

- Propose a self-supervised learning method with the additional MSE or Barlow twins loss in the intermediate layers generates higher quality representations than the standard MoCo in three different medical imaging tasks.
- The proposed methods improve the performance of the models in downstream classification tasks, especially on low label fractions of the data.
- The representations learned by the models are more reusable and informative compared to the standard MoCo (lower Kolmogorov–Smirnov distance).
- This work is the first to show the importance of intermediate layers in momentum contrastive self-supervised learning and in a diverse set of medical imaging tasks.

## Why

- How to learn a better representation in SSL in low-labeled data regime? This scenario is common in medical image.
- All the contrastive methods treat the backbone model as a black box and work with the final layer’s feature representations only, the paper hypothesize that ensuring closeness of representations for the intermediate layers, and not just the last one, significantly improves the learning of network parameters.

## How

![Screen Shot 2022-02-14 at 2.56.35 PM.png](Intermediate%20Layers%20Matter%20in%20Momentum%20Contrastive%20bad2b42b863e498e9aeb3b55dae9a2dd/Screen_Shot_2022-02-14_at_2.56.35_PM.png)

- Minimize the mean squared error between the intermediate layer representations or make their cross-correlation matrix closer to an identity matrix (Barlow Twins).
- For both intermediate loss function, negative pairs to learn the representations aren’t needed.
- Investigating the impact of the intermediate loss terms on feature quality, using state of the art analysis methods such as feature re-use, layer-wise probing and model output similarity.

### MSE

- Compute the mean squared error of the intermediate features between the two views of the same image. Specifically, extract the intermediate features and pass them through an adaptive average pooling layer to reduce the spatial variances in the two views that may be caused due to augmentations such as rotations.

### Cross-correlation

- Apply Barlow Twins loss to the intermediate layers, it is designed to bring the cross-correlation matrix of two feature representations close to an identity matrix.

### Analyze the features

- Fine tune the model using different fraction of labeled training data i.e. 1%, 6% and 100%.
- To objectively measure the quality, this paper investigate the re-usability of the features, probe the pre-trained models in a layer-wise manner, and compute the KS distance.
- To assess feature reuse in SSL, this paper measure the similarity of the features of the models trained by the proposed method, before and after fine tuning them on a labeled dataset.
- Layer-wise probing strategy: The entire network is frozen except the final linear classifier. Then extract features at the end of each ResNet block namely, "Block 1", "Block 2", "Block 3" and "Block 4”, these intermediate features are used to perform the downstream task, respectively.

## Results

- Features from the earlier blocks are more similar before and after finetuning, compared to the features in the later blocks for all the self-supervised learning methods, this shows the importance of intermediate layers
    
    
    ![Screen Shot 2022-02-14 at 3.12.08 PM.png](Intermediate%20Layers%20Matter%20in%20Momentum%20Contrastive%20bad2b42b863e498e9aeb3b55dae9a2dd/Screen_Shot_2022-02-14_at_3.12.08_PM.png)
    
- The proposed method perform better than MoCo in all the data-label fraction
    
    ![Screen Shot 2022-02-14 at 3.17.37 PM.png](Intermediate%20Layers%20Matter%20in%20Momentum%20Contrastive%20bad2b42b863e498e9aeb3b55dae9a2dd/Screen_Shot_2022-02-14_at_3.17.37_PM.png)
    
- There are higher feature similarity in the shallow layers of the model
    
    ![Screen Shot 2022-02-14 at 3.19.47 PM.png](Intermediate%20Layers%20Matter%20in%20Momentum%20Contrastive%20bad2b42b863e498e9aeb3b55dae9a2dd/Screen_Shot_2022-02-14_at_3.19.47_PM.png)
    
- Lower KS distance yields more informative features and better feature reusabilit
    
    ![Screen Shot 2022-02-14 at 3.24.22 PM.png](Intermediate%20Layers%20Matter%20in%20Momentum%20Contrastive%20bad2b42b863e498e9aeb3b55dae9a2dd/Screen_Shot_2022-02-14_at_3.24.22_PM.png)