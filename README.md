# Compress-Images-with-k-means-cluster

With the high demand on pictures through the internet, there is a need to compress pictures, so we can move them faster through our networks. There are various ways to compress pictures. In this project, we are using k-means, which is an unsupervised learning algorithm. There is more information available on k-means clustering in [Wikipedia](https://en.wikipedia.org/wiki/K-means_clustering).
Image Compression with k-means cluster is a way to compress an image from a 24 bit color presentation to a N bit for a 2^n color cluster.  Images comes with an RGB encoding that has 3 - 8 bit unsigned integer, from 0 to 255, which specifies red, green and blue intensity values.  The matrix for an RGB encoding is M(lines) x N(columns)  x 3(three color intensity).  Every pixel is a data example, so, for example, in a picture with 128 x 128 there is 16284 pixel, and each pixel has a three - 8 bit integer representing the colors.
The best way to graph an image  RGB encoding is by using the function scatter3 [scatter3Coding](compressImageCoding/scatter/scatter3Coding) from Matlab.  The picture below is a tree with 240 x 320 = 76800 pixels, each pixel has 3 numbers, from 1 to 256 and  each number represent the intensity of colors read, green and blue. The left image is a tree and the right image is the scatter3 graph representing the color distribution of the tree:

<img src="https://user-images.githubusercontent.com/53232113/115056922-0413cc00-9ea9-11eb-9453-ebb2c7b699b0.jpg" width="400" height="400"><img src="https://user-images.githubusercontent.com/53232113/115057013-21489a80-9ea9-11eb-8634-fb6734f6f7a9.jpg" width="400" height="400">

As seen, the intensity goes more to the color red(1-200) and blue(0-300) than the green color(1-100). There are 76800 pixels, with a combination of green-red-blue intensity color per pixel or data point.


With k-means algorithm, we could compress to into a N bit color that best group(cluster) the pixels for quality compressed images.  

The project analyzes two  different algorithms for compressing images and also shows the three dimensional distribution of scatter3 function in original, eight and two cluster images. 

Approach:

We are using two approaches for compression, one with Coursera Stanford Machine Learning Andrew Ng course code with some changes and other using kmeans, a Matlab internal functions.  This project compares the quality of images between these two approaches.

First Approach: Coursera Stanford Machine Learning by Andrew Ng code with some changes:
1. load image into an 3 dimensional  array (example: 2448 x 3264 x 3)
2. reshape into a 2 dimension array (example (7990272 x 3)
3. make array values from 0 to 1, dividing by 256 on the image structure
4. random initiatization of initial centroids(clusters of groups)................................ steps 1-4:  [initCompress](compressImageCoding/initCompress)
5. make a loop from 1 to maximum iterations you want (example = 10):
6. ------create vector m x 1 where m is the number of pixels, to assign each pixel to closest centroid
7. ------calculate new centroids (clusters or groups) with vector on 6 above..................... steps 5=7:  [CentroidLoop](compressImageCoding/centroidLoop)
8. find final centroid assigmments, vector m x 1  ................................................   step 8:  [findClosestCentroid](compressImageCoding/findClosestCentroid)
9. reconstruct the image based on final centroid assigment on 8 above
10. convert recovered image into initial dimensions (example: from 7990272 x 3   to 2448 x 3264 x 3)
11. save image, write into disk and show image  .................................................. steps 9-11 [writeImageFile](compressImageCoding/writeImageFile)
12. Do steps from 1 to 11 with cluster = 4,8,16,32
13. show images: original and compare with 32 centroids, 16 centroids, 8 centroids, and 4 centroids cluster images.

Here, there are five pictures from left to right: original, 32, 16 ,8 and 4 compress cluster images:

<img src="https://user-images.githubusercontent.com/53232113/114751253-87eb7e00-9d1a-11eb-846d-c2312a78d2e4.JPG"  width="200" height="280"> <img src="https://user-images.githubusercontent.com/53232113/114776216-d9eecc80-9d37-11eb-9f64-04a24b9f5c20.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114785729-b67d4f00-9d42-11eb-9d20-107e708ea9b6.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114786526-dd885080-9d43-11eb-9adc-27c60c3cbb63.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114788600-5dfc8080-9d47-11eb-9087-b7127815f5b2.jpg" width="200" height="280">
<img src="https://user-images.githubusercontent.com/53232113/114796500-bd15c180-9d56-11eb-91d9-4b479d9f8ec9.jpg" width="1000" height="100">

Observations
1. it is a pretty big pixel picture with almost 8 millon pixels.
2. the time to process the algorithm is between 10 seconds to one minute.
3. for initial cluster it is used a randperm(m) function. This function gets a random number from 0 to m in the vector matrix, then gets the first K numbers. Every time the randperm function is run, gets different numbers.
4. for each pixel, there is a IDX vector that point to the closest cluster centroids by finding all the data points for each centroid and getting the mean of all X data in ths cluster. This is the assignment step where each data point is assigned to a cluster whose center is nearest to it.
5. to find a new K clusters, the routine computeCentroids gets centroids by finding all the data points for each centroid and getting the mean of all  
6. the assignmment step and update step, both,   repeat 10 iterations until it finds the final IDX vector corresponding to final K clusters
7. the final X_compressed matrix has [n x 1] dimensions where n is the number of pixels in the image.  Note that this matrix has the same size for any clusters, the difference is just the numbers on it. For example, if there is a 16 cluster group, there will be just 16 values on the matrix. The way to check is by using unique(X) where X is the compressed matrix.
8. finally this matrix is converted from  a double matrix into an image PngFile.jpg, write the image  on disk, and finally  show image on screen. 
9. in k-means cluster compression there is always a picture degradation and is necessary find the best compression with the least degradation.


Conclusions:
1. the 32 cluster picture is very similar to the original and has 49% of the original size kbytes, the 16, 8 and 4 cluster images, are not so clear and the sizes are very similar to the 32 cluster picture.
2. With this particular image, the correct cluster to compress the size in 49%  of the original is a 32 cluster grouping.


Second Approach: use kmeans, a Matlab internal function, for image compression
1. load image into an 3 dimensional  array (example: 2448 x 3264 x 3)
2. reshape into a 2 dimension array (example (7990272 x 3)
3. make array values from 0 to 1, dividing by 256 on the image structure
4. initialize k=number of cluster, number of replicates until finding the best cluster
5. use kmeans function and get as output the assignment vector idx and the centroid values
6. convert recovered image into initial dimensions (example: from 7990272 x 3   to 2448 x 3264 x 3)
7. save image, write into disk and show image ............................................ steps 1 to 7 in [kMeansApproach](compressImageCoding/KmeansApproach)
8. Do steps from 1 to 7 with cluster = 4,8,16,32
14. show images: original and compare with 32 centroids, 16 centroids, 8 centroids, and 4 centroids cluster images.

Here, there are five pictures from left to right> original, 32, 16 ,8 and 4 compress cluster images using kmean: 

<img src="https://user-images.githubusercontent.com/53232113/114751253-87eb7e00-9d1a-11eb-846d-c2312a78d2e4.JPG"  width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114955593-a341b080-9e22-11eb-97b3-86aaf53923e6.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114955648-c3716f80-9e22-11eb-8cdd-6e019967e471.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114955682-d5531280-9e22-11eb-864e-1a21d21d656a.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114955712-e439c500-9e22-11eb-9aed-074989e24d1e.jpg" width="200" height="280">
<img src="https://user-images.githubusercontent.com/53232113/114957256-45af6300-9e26-11eb-8c6e-0c4f270ff63c.jpg" width="1000" height="100">

Observations:
1.- the kmeans function used has 10 replicates and 10 maximun iteration. 
2. the time to process is between two minutes and ten minutes.

Conclusions:
1.- Best compression with K = 32, decreases size from 2689 to 1893, 42 %.
2.- K = 32 is the best quality picture compared with the original.
3.- k = 16 or less: there is an important degradation in the images.
4.- kmeans algorithm is slow.

Differences in quality pictures between two approaches(top is Stanford codign and botton is kmeans Matlab function):
<img src="https://user-images.githubusercontent.com/53232113/114751253-87eb7e00-9d1a-11eb-846d-c2312a78d2e4.JPG"  width="200" height="280"> <img src="https://user-images.githubusercontent.com/53232113/114776216-d9eecc80-9d37-11eb-9f64-04a24b9f5c20.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114785729-b67d4f00-9d42-11eb-9d20-107e708ea9b6.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114786526-dd885080-9d43-11eb-9adc-27c60c3cbb63.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114788600-5dfc8080-9d47-11eb-9087-b7127815f5b2.jpg" width="200" height="280">
<img src="https://user-images.githubusercontent.com/53232113/114796500-bd15c180-9d56-11eb-91d9-4b479d9f8ec9.jpg" width="1000" height="100">
<img src="https://user-images.githubusercontent.com/53232113/114751253-87eb7e00-9d1a-11eb-846d-c2312a78d2e4.JPG"  width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114955593-a341b080-9e22-11eb-97b3-86aaf53923e6.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114955648-c3716f80-9e22-11eb-8cdd-6e019967e471.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114955682-d5531280-9e22-11eb-864e-1a21d21d656a.jpg" width="200" height="280"><img src="https://user-images.githubusercontent.com/53232113/114955712-e439c500-9e22-11eb-9aed-074989e24d1e.jpg" width="200" height="280">
<img src="https://user-images.githubusercontent.com/53232113/114957256-45af6300-9e26-11eb-8c6e-0c4f270ff63c.jpg" width="1000" height="100">

Observations of comparison:
1. on first approach with modified Stanford code there is no replicates and 10 iterations, and on the second approach with kmeans function there are 10 replicates and 10 iterations.
2. Compressed pictures with Stanford code have much better quality than compressed pictures with kmeans function.
3. In Stanford coding the best quality picture is with K=32 with a 49 percent decrease in image size.
4. In Kmeans coding the best quality picture is with K=32 with a 42 percent decrease in image size, with a poor quality picture.

Conclusion of differences in k-means clustering between Stanford coding and kmeans Matlab function

The Stanford coding for compressing images with  k-means clustering has much better results in quality, size and time to process than  kmeans Matlab function.

Scatter3 function

The Scatter3 function [Scatter3Coding](compressImageCoding/scatter/scatter3Coding) creates a plot in three dimensions that shows each pixel or data point in the image with its  three (red, green, blue) color intensity. It is a good way to see the distribution of color of an image. The ilustriations below shows how this scatter3 image changes in an original and compress images(8 cluster and 2 cluster): 

<img src="https://user-images.githubusercontent.com/53232113/115056922-0413cc00-9ea9-11eb-9453-ebb2c7b699b0.jpg" width="150" height="150"><img src="https://user-images.githubusercontent.com/53232113/115057013-21489a80-9ea9-11eb-8634-fb6734f6f7a9.jpg" width="170" height="200"><img src="https://user-images.githubusercontent.com/53232113/115057052-302f4d00-9ea9-11eb-815c-b4d629e99bf8.jpg" width="170" height="200"><img src="https://user-images.githubusercontent.com/53232113/115057100-40dfc300-9ea9-11eb-940b-25e0a69f6fb8.jpg" width="170" height="200"><img src="https://user-images.githubusercontent.com/53232113/115057158-5228cf80-9ea9-11eb-8cdd-f084b898cc53.jpg" width="170" height="200"><img src="https://user-images.githubusercontent.com/53232113/115057214-64a30900-9ea9-11eb-8c9d-c72c60b03da9.jpg" width="170" height="200">

On the original  image the color intensity on green is between 0-150, on red between 0-200 and on blue between 0-280.
On the 8-cluster image the color intensity on green is between 0-100, on red between 0-150 and on blue between 0-280.
On the 2-cluster image the color intensity on green is betwwen 0-100, on red between 0-100 and on blue between 0-300.

On the original picture there is a wide range in red, on the 8 cluster picture there is thin range on green and red and on the 2 cluster picture thre is thin range on green and red and wide range in blue.










  

