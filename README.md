# Style_Transfer
Convolutional Neural Networks consist of layers of small computational units that process visual information hierarchically in a feed forward manner. Each layer of units can be understood as a collection of image filters, each of which extracts a certain feature from the input image.  
There are 2 input images namely content image and style image that are used to generate an output image called stylized image. This image has same content as content image and has style similar to style image. To make sure that content image(C) and generated image(G) are similar with respect to their content and not style, while on the other hand make sure that generated image only inherits similar style representation from style image(S) and not the entire style image itself, the loss function is divied into 2 parts, content loss and style loss.<br>
<p align='center'>
  <b>
    L<sub>total</sub> (S,C,G) = α L<sub>content</sub> (C,G) + β L<sub>style</sub> (S,G)
  </b>
</p><br>
Alpha and beta are hyperparameters which are used to provide weights to each type of loss i.e these parameters are used to control how much of content/style we want to inherit in the generated image.<br>

**VGG-19**<br>
![alt text](https://www.researchgate.net/profile/Clifford-Yang/publication/325137356/figure/fig2/AS:670371271413777@1536840374533/llustration-of-the-network-architecture-of-VGG-19-model-conv-means-convolution-FC-means.jpg)

## Extract Content:
* Along the processing hierarchy of the network, the input image is transformed into representations that increasingly care about the actual content of the image compared to its detailed pixel values.
* We therefore refer to the feature responses in higher layers of the network as the content representation.
* The second part of fourth (4_2) convolutional layer of pre-trained VGG-19 network is used as content extractor.

## Extract Style:
* To obtain a representation of the style of an input image, we use correlations between the different filter responses over the spatial extent of the feature maps. We obtain a stationary, multi-scale representaion of the input image, which captures its texture information but not the global arrangement.
* The correlations between feature maps is known as gram matrix.
* The layers used for calculation of gram matrix are 1_1, 2_1, 3_1, 4_1, 5_1 with varied style weight constant for each layer.
