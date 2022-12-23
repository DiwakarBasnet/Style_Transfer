# Style_Transfer
There are 2 input images namely content image and style image that are used to generate an output image called stylized image. This image has same content as content image and has style similar to style image. To make sure that content image(C) and generated image(G) are similar with respect to their content and not style, while on the other hand make sure that generated image only inherits similar style representation from style image(S) and not the entire style image itself, the loss function is divied into 2 parts, content loss and style loss.<br>
<p align='center'>
  <b>
    L<sub>total</sub>(S,C,G) = αL<sub>content</sub>(C,G) + βL<sub>style</sub>(S,G)
  </b>
</p>
