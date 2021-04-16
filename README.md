# Compress-Images-with-k-means-cluster

With the high demand on pictures through the internet, there is a need to compress pictures, so we can move them faster through our networks. There are various ways to compress pictures. In this project, we are using k-means, which is an unsupervised learning algorithm.
Image Compression with k-means cluster is a way to compress an image from a 24 bit color presentation to a N bit for a 2^n color cluster.  Images comes with an RGB encoding that has 3 - 8 bit unsigned integer, from 0 to 255, which specifies red, green and blue intensity values.  The matrix for an RGB encoding is M(lines) x N(columns)  x 3(three color intensity).  Every pixel is a data example, so, for example, in a picture with 128 x 128 there is 16284 pixel, and each pixel has a three - 8 bit integer representing the colors.
With k-means algorithm, we could compress to into a N bit color that best group(cluster) the pixels.  

In this project, We will analyze two different algorithms for compressing images and, finally, demostrate the use of  scatter3 function, which plots in three dimensions the red-green-blue image color intensity. 

Approach:

We are using two approaches for compression, one with Coursera Standord Machine Learning Andrew Ng course code with some changes and other using kmeans, a Matlab internal functions.  This project compares the quality of images between these two approaches.

First Approach: Coursera Stanford Machine Learning by Andrew Ng code with some changes:
1. load image into an 3 dimensional  array (example: 2448 x 3264 x 3)
2. reshape into a 2 dimension array (example (7990272 x 3)
3. make array values from 0 to 1, dividing by 256 on the image structure
4. random initiatization of initial centroids(clusters of groups)................................ steps 1-4:  initCompress(see compressImageCoding)
5. make a loop from 1 to maximum iterations you want (example = 10):
6. ------create vector m x 1 where m is the number of pixels, to assign each pixel to closest centroid
7. ------calculate new centroids (clusters or groups) with vector on 6 above..................... steps 5=7:  CentroidLoop(see compressImageCoding)  .
8. find final centroid assigmments, vector m x 1  ................................................   step 8:  findClosestCentroid(see CompressImageCoding)
9. reconstruct the image based on final centroid assigment on 8 above
10. convert recovered image into initial dimensions (example: from 7990272 x 3   to 2448 x 3264 x 3)
11. save image, write into disk and show image  .................................................. steps 9-11 writeImageFile(see CompressImageCoding)
12. Do steps from 1 to 11 with cluster = 4,8,16,32
13. show images: original and compare with 32 centroids, 16 centroids, 8 centroids, and 4 centroids cluster images.

Here, there are five pictures from left to right> original, 32, 16 ,8 and 4 compress cluster images:

<img src="https://user-images.githubusercontent.com/53232113/114751253-87eb7e00-9d1a-11eb-846d-c2312a78d2e4.JPG"  width="200" height="280"> <img src="https://user-images.githubusercontent.com/53232113/114776216-d9eecc80-9d37-11eb-9f64-04a24b9f5c20.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114785729-b67d4f00-9d42-11eb-9d20-107e708ea9b6.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114786526-dd885080-9d43-11eb-9adc-27c60c3cbb63.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114788600-5dfc8080-9d47-11eb-9087-b7127815f5b2.jpg" width="200" height="280">
<img src="https://user-images.githubusercontent.com/53232113/114796500-bd15c180-9d56-11eb-91d9-4b479d9f8ec9.jpg" width="1000" height="100">

Observations
1. it is a pretty big pixel picture with almost 8 millon pixels
2. for initial cluster it is used a randperm(m) function. This function gets a random number from 0 to m in the vector matrix, then gets the first K numbers. Every time the randperm function is run, gets different numbers.
3. for each pixel, there is a IDX vector that point to the closest cluster centroids by finding all the data points for each centroid and getting the mean of all X data in ths cluster. This is the assignment step where each data point is assigned to a cluster whose center is nearest to it.
4. to find a new K clusters, the routine computeCentroids gets centroids by finding all the data points for each centroid and getting the mean of all  
5. the assignmment step and update step, both,   repeat 10 iterations until it finds the final IDX vector corresponding to final K clusters
6. the final X_compressed matrix has [n x 1] dimensions where n is the number of pixels in the image.  Note that this matrix has the same size for any clusters, the difference is just the numbers on it. For example, if there is a 16 cluster group, there will be just 16 values on the matrix. The way to check is by using unique(X) where X is the compressed matrix.
7. finally this matrix is converted from  a double matrix into an image PngFile.jpg, write the image  on disk, and finally  show image on screen. 

Conclusions:
1. the 32 cluster picture is very similar to the original and has almost half the size in kbytes, the 16, 8 and 4 cluster images, are not so clear and the sizes are very similar to the 32 cluster picture.
2. With this particular image, the correct cluster to compress the size in almost half of the original is a 32 cluster grouping.
3. in k-means cluster compression there is always a picture degradation and is necesary find the best compression with the least degradation.

Second Approach: use kmeans, a Matlab internal function, for image compression

1. load image into an 3 dimensional  array (example: 2448 x 3264 x 3)
2. reshape into a 2 dimension array (example (7990272 x 3)
3. make array values from 0 to 1, dividing by 256 on the image structure
4. initialize k=number of cluster, number of replicates until finding the best cluster
5. use kmeans function and get as output the assignment vector idx and the centroid values
6. convert recovered image into initial dimensions (example: from 7990272 x 3   to 2448 x 3264 x 3)
7. save image, write into disk and show image
8. Do steps from 1 to 7 with cluster = 4,8,16,32
14. show images: original and compare with 32 centroids, 16 centroids, 8 centroids, and 4 centroids cluster images.

Note that the kmeans function used has 10 replicates and 10 maximun iteration. Here, there are five pictures from left to right> original, 32, 16 ,8 and 4 compress cluster images using kmean: 

<img src="https://user-images.githubusercontent.com/53232113/114751253-87eb7e00-9d1a-11eb-846d-c2312a78d2e4.JPG"  width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114955593-a341b080-9e22-11eb-97b3-86aaf53923e6.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114955648-c3716f80-9e22-11eb-8cdd-6e019967e471.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114955682-d5531280-9e22-11eb-864e-1a21d21d656a.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114955712-e439c500-9e22-11eb-9aed-074989e24d1e.jpg" width="200" height="280">
<img src="https://user-images.githubusercontent.com/53232113/114957256-45af6300-9e26-11eb-8c6e-0c4f270ff63c.jpg" width="1000" height="100">

Conclusions:
1.- Best compression with K = 32, decreases size from 2689 to 1893, 42 %.
2.- K = 32 is the best quality picture compared with the original
3.- k = 16 or less: there is an important degradation in the images.


Differences in quality pictures between two approaches:
With Stanford coding:

<img src="https://user-images.githubusercontent.com/53232113/114751253-87eb7e00-9d1a-11eb-846d-c2312a78d2e4.JPG"  width="200" height="280"> <img src="https://user-images.githubusercontent.com/53232113/114776216-d9eecc80-9d37-11eb-9f64-04a24b9f5c20.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114785729-b67d4f00-9d42-11eb-9d20-107e708ea9b6.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114786526-dd885080-9d43-11eb-9adc-27c60c3cbb63.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114788600-5dfc8080-9d47-11eb-9087-b7127815f5b2.jpg" width="200" height="280">
<img src="https://user-images.githubusercontent.com/53232113/114796500-bd15c180-9d56-11eb-91d9-4b479d9f8ec9.jpg" width="1000" height="100">

With kmeans function:

<img src="https://user-images.githubusercontent.com/53232113/114751253-87eb7e00-9d1a-11eb-846d-c2312a78d2e4.JPG"  width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114955593-a341b080-9e22-11eb-97b3-86aaf53923e6.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114955648-c3716f80-9e22-11eb-8cdd-6e019967e471.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114955682-d5531280-9e22-11eb-864e-1a21d21d656a.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114955712-e439c500-9e22-11eb-9aed-074989e24d1e.jpg" width="200" height="280">
<img src="https://user-images.githubusercontent.com/53232113/114957256-45af6300-9e26-11eb-8c6e-0c4f270ff63c.jpg" width="1000" height="100">

Observations of comparison:
1. on first approach with modified Stanford code there is no replicates and 10 iterations, and on the second approach with kmeans function there are 10 replicates and 10 iterations.
2. Compressed pictures with Stanford code have much better quality than compressed pictures with kmeans function.
3. In Stanford coding the best quality picture is with K=32 with a 49 percent decrease in image size.
4. In Kmeans coding the best quality picture is with K=32 with a 42 percent decrease in image size, with a poor quality picture.

Conclusion of differences in k-means clustering between Stanford coding and kmeans Matlab function

The Stanford coding for compressing images with  k-means clustering has much better results in quality and size of compression than kmeans Matlab function.  

6. 
7. 




  

