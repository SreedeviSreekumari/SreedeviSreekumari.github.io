---
layout: post
title: Image Manipulation
description: Crop,Flip and Stack image using Python-Numpy 
image: "/posts/camaro.jpg"
tags: [Python, Numpy, Matpotlib]
---

In this post let's explore the power of Numpy with images.

```ruby
import numpy as np
from skimage import io
import matplotlib.pyplot as plt
```

Read the image required for manipulation using 'imread' function and specify the image location.

```ruby
camaro = io.imread("camaro.jpg")
print(camaro)
```
Result of the print will be an array of values as below which constitute the camaro.jpg.

[[[ 83  81  43]
  [ 57  54  19]
  [ 34  31   0]
  ...
  [179 144 112]
  [179 144 114]
  [179 144 114]]

 [[ 95  93  55]
  [ 72  69  34]
  [ 46  43   8]
  ...
  [181 146 114]
  [181 146 116]

Let's find out what shape is camaro object.

```ruby
camaro.shape
```
Shape of camaro object here is (1200,1600,3) which means 1200 rows,1600 columms and 3 dimensions.
The third dimension here is pixel intensity for which integer values range from integer 0 to 255.

```ruby
# Display image and plot the object 
  plt.imshow(camaro)
  plt.show
```
<img src="https://raw.githubusercontent.com/SreedeviSreekumari/SreedeviSreekumari.github.io/master/img/posts/camaro.jpg">

```ruby
# Crop the image vertically and display the image. This would mean that y axis will be affected.
  cropped = camaro[0:500,:,:]
  plt.imshow(cropped)
  plt.show
```
<img src="https://raw.githubusercontent.com/SreedeviSreekumari/SreedeviSreekumari.github.io/master/img/posts/camaro_vertical_crop.jpg">

```ruby
# Crop the image horizontally and display the image. This would mean that x axis will be affected.
  cropped = camaro[:,0:500,:]
  plt.imshow(cropped)
  plt.show
```
<img src="https://raw.githubusercontent.com/SreedeviSreekumari/SreedeviSreekumari.github.io/master/img/posts/camaro_horizontal_crop.jpg">

```ruby
# Now let's try to crop just the car perfectly
  cropped = camaro[350:1100,200:1400,:]
  plt.imshow(cropped)
  plt.show
```
<img src="https://raw.githubusercontent.com/SreedeviSreekumari/SreedeviSreekumari.github.io/master/img/posts/camaro_cropped.jpg">

```ruby
# To save the image to disk
  io.imsave("camaro_cropped.jpg",cropped)
```
We can flip the image by reversing the rows/columns and keeping the color channel untouched. 
A vertical flip reverses the rows where as a horizongtal flip reverses columns.
To indicate which flip we are looking for, use -1 in the designated position.

```ruby
# Vertical flip
  vertical_flip = camaro[::-1,:,:]
# Display flipped image
  plt.imshow(vertical_flip)
  plt.show
```
<img src="https://raw.githubusercontent.com/SreedeviSreekumari/SreedeviSreekumari.github.io/master/img/posts/camaro_vertical_flip.jpg">

```ruby
# Save vertically flipped image
  io.imsave("camaro_vertical_flip.jpg",vertical_flip)
```
```ruby
# Horizontal flip
  horizontal_flip = camaro[:,::-1,:]
# Display flipped image
  plt.imshow(horizontal_flip)
  plt.show
```
<img src="https://raw.githubusercontent.com/SreedeviSreekumari/SreedeviSreekumari.github.io/master/img/posts/camaro_horizontal_flip.jpg">

```ruby
# Save horizontally flipped image
  io.imsave("camaro_horizontal_flip.jpg",horizontal_flip)
```
We should keep in mind that the Color channels available are red,green and blue. We can now try to manipulate the original image with only red channels populated while keeping other color channels as zero. For this, we need to create a numpy array same as the original array,but with array value as zeroes and then populating only red channels.
```ruby
red = np.zeros(camaro.shape,dtype = "uint8")
``` 

We have created an array 'red' with same dimension as the original image.Now we want to populate only red channel and will keep other color channels zero.
```ruby
red[:,:,0] = camaro[:,:,0]
plt.imshow(red)
plt.show
```   
<img src="https://raw.githubusercontent.com/SreedeviSreekumari/SreedeviSreekumari.github.io/master/img/posts/camaro_red_channel.jpg">

Now let's repeat this for green and blue channels.
```ruby
green = np.zeros(camaro.shape,dtype = "uint8")  
green[:,:,1] = camaro[:,:,1]
plt.imshow(green)
plt.show
```  
<img src="https://raw.githubusercontent.com/SreedeviSreekumari/SreedeviSreekumari.github.io/master/img/posts/camaro_green_channel.jpg">

```ruby
blue = np.zeros(camaro.shape,dtype = "uint8")  
blue[:,:,2] = camaro[:,:,2]
plt.imshow(blue)
plt.show
```  
<img src="https://raw.githubusercontent.com/SreedeviSreekumari/SreedeviSreekumari.github.io/master/img/posts/camaro_blue_channel.jpg">

``` 
In numpy, it is possible to stack arrays vertically and horizontally. Right now, we have the image as numpy array values with us. Let's see how we can stack them.
```ruby
# Vertically stacking the images that we created with color channels - red,green and blue
  camaro_rainbow_vstack = np.vstack((red,green,blue))
  plt.imshow(camaro_rainbow_vstack)
  plt.show
```
<img src="https://raw.githubusercontent.com/SreedeviSreekumari/SreedeviSreekumari.github.io/master/img/posts/camaro_vstack.jpg">

```ruby
# Save the vertically stacked image
  io.imsave("camaro_vstack.jpg",camaro_rainbow_vstack)
``` 

```ruby
# Horizontal stacking the images that we created with color channels - red,green and blue
  camaro_rainbow_hstack = np.hstack((red,green,blue))
  plt.imshow(camaro_rainbow)
  plt.show
```
<img src="https://raw.githubusercontent.com/SreedeviSreekumari/SreedeviSreekumari.github.io/master/img/posts/camaro_hstack.jpg">

```ruby
# Save the horizontally stacked image
io.imsave("camaro_hstack.jpg",camaro_rainbow_hstack)
```
