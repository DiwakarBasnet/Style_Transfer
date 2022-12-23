# Style_Transfer
There are 2 input images namely content image and style image that are used to generate an output image called stylized image. This image has same content as content image and has style similar to style image. To make sure that content image(C) and generated image(G) are similar with respect to their content and not style, while on the other hand make sure that generated image only inherits similar style representation from style image(S) and not the entire style image itself, the loss function is divied into 2 parts, content loss and style loss.<br>
<p align='center'>
  <b>
    L<sub>total</sub> (S,C,G) = α L<sub>content</sub> (C,G) + β L<sub>style</sub> (S,G)
  </b>
</p>
Alpha and beta are hyperparameters which are used to provide weights to each type of loss i.e these parameters are used to control how much of content/style we want to inherit in the generated image.
