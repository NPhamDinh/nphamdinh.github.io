---
layout: page
title: Malware Detection
description: Files are converted into images and then classified by a CNN to identify Malware.
img: assets/img/malware_preview.jpg
importance: 3
category: fun
---

When it comes to malware, there are two ways to play detective: dynamic and static analysis. One involves running suspicious software in a virtual playground to see how it behaves, and the other looks at the malware's characteristics without letting it run wild. Traditional methods, like checking hash values in a database, have their limits as new malware pops up all the time.

But here's where it gets interesting: back in high school, I stumbled upon a cool <a href="https://doi.org/10.1145/2016904.2016908">idea</a> from Nataraj et al. Instead of sifting through lines of code, what if we turned it into a picture? We're talking about representing a file's binary code as a grayscale image. Interestingly, it transforms malware analysis into an image recognition game.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/malware_goodware.jpg" title="" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Can you see the difference between malware and goodware?
</div>


These representations are being created by converting every 8 Bits of a file into a greyscale value for a pixel. Taking advantage of that lead to a hobby project in my high school days. The original paper classified these with GIST feature extraction and k-nearest-neighbour. Henceforth, I decided to use CNNs for that and outperform the previous accuracies. 
Moreover, the FC-layers of CNNs require the inputs to be of same size. Due to programs being of different lenghts, I decided to not only scale the images to the same size, but also compare the approach of using spatial pyramid pooling for this matter. 

| Dataset | Resizing | Spatial Pyramid Pooling | Adaptive Max Pooling |
|----------|----------|----------|
| Malimg (25 virus families) | 98.07% | 96.79% | 94.97% |
| MS Malware (9 virus families) | 97.33% | 90.71% | 88.78 % |
| Raw PE (binary) | 82.54%| 83.53 %| 78.17 % |

<div class="caption">
    Accuracies of the CNN on the datasets with different strategies to approach inputs of different sizing
</div>

<center><img src="/assets/img/malware_preview.png" width="300" height="300" /> </center>

<div class="caption">
    Representation of two virus families
</div>

Thus, resizing all images to the same size (256x256) appears to perform best for classifying virus families. The spatial pyramid pooling lead to the best accuracy for distinguishing malware and goodware. Regardless of the domain, examining other approaches to handle the matter of having inputs of different sizes for a classifier was quite thrilling. Shoutout to my school mate Jan P. Große who did it together with me.



