# Compress-Images-with-k-means-cluster

With the high demand on pictures through the internet, there is a need to compress pictures, so we can move them faster through our networks. There are various ways to compress pictures. In this project, we are using k-means, which is an unsupervised learning algorithm.
Image Compression with k-means cluster is a way to compress an image from a 24 bit color presentation to a N bit for a 2^n color cluster.  Images comes with an RGB encoding that has 3 - 8 bit unsigned integer, from 0 to 255, which specifies red, green and blue intensity values.  The matrix for an RGB encoding is M(lines) x N(columns)  x 3(three color intensity).  Every pixel is a data example, so, for example, in a picture with 128 x 128 there is 16284 pixel, and each pixel has a three - 8 bit integer representing the colors.
With k-means algorithm, we could compress to into a N bit color that best group(cluster) the pixels.  

Approach:

We are using two approaches for compression, one with Coursera Standord Machine Learning Andrew Ng course code with some changes and other using Matlab internal functions.  Both approaches get a similar picture quality.  

First Approach: Coursera Stanford Machine Learning by Andrew Ng code with some changes:
1. load image into an 3 dimensional  array (example: 128 x 128 x 3)
2. reshape into a 2 dimension array (example (16384 x 3)
3. make array values from 0 to 1, dividing by 256 o 256x256 depending on the image structure
4. random initiatization of initial centroids(clusters of groups)
5. make a loop from 1 to maximum iterations you want (example = 10):
6. ------create vector m x 1 where m is the number of pixels, to assign each pixel to closest centroid
7. ------calculate new centroids (clusters or groups) with vector on 6 above
8. find final centroid assigmments, vector m x 1
9. reconstruct the image based on final centroid assigment on 8 above
10. convert recovered image into initial dimensions (example: from 16384 x 3   to 128 x 128 x 3)
11. save image, write into disk and show image
12. Do steps from 1 to 11 with cluster = 2,4,8, and 16
13. show picture size with 2,4,8, and 16 cluster (or colors) compared with original image.

Here, there are five pictures from left to right> original, 32, 16 ,8 and 4 compress cluster images:

<img src="https://user-images.githubusercontent.com/53232113/114751253-87eb7e00-9d1a-11eb-846d-c2312a78d2e4.JPG"  width="200" height="300"> <img src="https://user-images.githubusercontent.com/53232113/114776216-d9eecc80-9d37-11eb-9f64-04a24b9f5c20.jpg" width="200" height="300"><img src="https://user-images.githubusercontent.com/53232113/114785729-b67d4f00-9d42-11eb-9d20-107e708ea9b6.jpg" width="200" height="300"><img src="https://user-images.githubusercontent.com/53232113/114786526-dd885080-9d43-11eb-9adc-27c60c3cbb63.jpg" width="200" height="300"><img src="https://user-images.githubusercontent.com/53232113/114788600-5dfc8080-9d47-11eb-9087-b7127815f5b2.jpg" width="200" height="300">
<img src="https://user-images.githubusercontent.com/53232113/114796500-bd15c180-9d56-11eb-91d9-4b479d9f8ec9.jpg" width="1000" height="100">









Second Approach: using octave internal functions       

