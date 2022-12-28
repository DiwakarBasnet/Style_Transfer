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
![VGG-19 layers](https://raw.githubusercontent.com/DiwakarBasnet/Style_Transfer/main/VGG-19.jpg?token=GHSAT0AAAAAABYAO27KKLDR3CPCMOZ4SARUY5GR4EQ)

## Extract Content:
* Along the processing hierarchy of the network, the input image is transformed into representations that increasingly care about the actual content of the image compared to its detailed pixel values.
* We therefore refer to the feature responses in higher layers of the network as the content representation.
* The second part of fourth (4_2) convolutional layer of pre-trained VGG-19 network is used as content extractor.

## Extract Style:
* To obtain a representation of the style of an input image, we use correlations between the different filter responses over the spatial extent of the feature maps. We obtain a stationary, multi-scale representaion of the input image, which captures its texture information but not the global arrangement.
* The correlations between feature maps is known as gram matrix.
* The layers used for calculation of gram matrix are 1_1, 2_1, 3_1, 4_1, 5_1 with varied style weight constant for each layer.

## Content Loss:
Let's say we have function Content loss which takes in three arguments as input that are content image "p", generated image "x" and the layer "l" whose activation we are going to use to compute loss.<br>
<p align='center'>
  <b>
    $$L_{content} \left( p,x,l \right) =  {1 \over 2} \sum_{ij} \left( F_{ij}^l - P_{ij}^l \right)^2$$
  </b>
</p><br>
Where 
$$F_{ij}^l$$ 
is the activation of the 
$$i^{th}$$ 
filter at position j in layer l for generated image, similarly 
$$P_{ij}^l$$ 
is the feature representation for content image.

## Gram Matrix:
To get the correlation of all the channels w.r.t each other we need to calculate gram matrix, we will use gram matrix to measure the degree of correlation between channels which later will act as a measure of style itself.<br>
<p align='center'>
  <b>
    $$G_{ij}^l = \sum_{k} F_{ik}^l F_{jk}^l$$
  </b>
</p><br>
In simple words, a gram matrix is a matrix created by multiplying a matrix with it's own transpose. The dot product of transpose of matrix created by vector of feature maps and matrix itself gives gram matrix.

## Style Loss:
While computing style loss we use multiple activation layers, that scenarios leads us to a possibility of assigning different weightages to each sub loss provided by different layers but in most cases people give equal weightage for all layers.<br>
<p align='center'>
  <b>
    $$E_l = {1 \over 4 N_l^2 M_l^2} \sum_{ij} \left( G_{ij}^l - A_{ij}^l \right)^2 <br>
    L_{style} \left( a,x \right) = \sum_{l=0}^L w_l * E_l$$
  </b>
</p><br>
Where "a" and "x" are style image and generated image and 
$$A^l and G^l$$ 
are their respective style representations in layer l.
