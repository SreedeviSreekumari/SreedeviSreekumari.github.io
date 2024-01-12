---
layout: post
title: Calculating Planet Volume
description: Using Python Numpy to calculate Planet Volumes
image: "/posts/Planet_Volume.jpg"
tags: [Python, Numpy]
---

In this post I'm going to show you how powerful Numpy can be. Let's find out how to calculate volume of planets using numpy with Python. As we all know, we have 8 planets and we aim to calculate volume of each one of them. To calculate the volume, the formula is

```ruby
Volume = 4/3 * pi * radii ** 3
```
So here, we would need pi value and radii for volume computation.

As per google data, radii of planets (in kilometers) are as follows.

Mercury - 2439.7 |
Venus 	- 6051.8  |
Earth 	- 6371    |
Mars 	  - 3389.7 |
Jupiter - 69911  |
Saturn	- 58232   |
Uranus	- 25362   |
Neptune	- 24622

Let's see how can we use this data for calculation.

```ruby
import numpy as np

# Store all the radii data we have in a numpy array and keep the array name as 'radii'
radii = np.array([2439.7, 6051.8, 6371, 3389.7, 69911, 58232, 25362, 24622])
print(radii)
>>> [ 2439.7  6051.8  6371.   3389.7 69911.  58232.  25362.  24622. 

# Calculate planet volume using the formula.
# Instead of directly using a Pi value, we can make use of numpy function to achieve the same.
volumes = 4/3 * np.pi * radii ** 3

# Let's print and see what values the numpy array hold.
print(volumes)
>>>
[6.08272087e+10 9.28415346e+11 1.08320692e+12 1.63144486e+11
 1.43128181e+15 8.27129915e+14 6.83343557e+13 6.25257040e+13]
```
Notice here that volume has been calculated for each element of the numpy array without the need for a loop or index.

Now, let's extend the code and see how we could find volume of a million planets just by assuming the radii. For this, we will make use of 'randint' function, which will assign random numbers as planet radii. We can also specify the range of random numbers for radii assumption.In the below example, we are assigning an array with random values between the range of 1 and 1000 assuming we need to calculate volume for a million planets.Then calculate volume using the previous formula.

```ruby
radii = np.random.randint(1,1000,1000000)
volumes = 4/3 * np.pi * radii ** 3
print(volumes)
>>>
[2.87309120e+04 2.48271271e+09 5.23598776e+02 ... 1.84765190e+07
 1.13976057e+09 3.47914212e+09]
```

We now have volume of millions of planets! How wonderful is that?! 
I hope you found the the use of Numpy in Python interesting.
