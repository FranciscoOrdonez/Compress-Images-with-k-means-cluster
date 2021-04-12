# Compress-Images-with-k-means-cluster

With the high demand on pictures through the internet, there is a need to compress pictures, so we can move them faster through our networks. There are various ways to compress pictures. In this project, we are using k-means algorith.  
Image Compression with k-means cluster is a way to compress an image from a 24 bit color presentation to a 4 bit.  Images comes with an RGB encoding that has 3 - 8 bit
unsigned integer, from 0 to 255, which specifies red, green and blue intensity values.  The matrix for an RGB encoding is 128 x 128 x 3(three color intensity).  Every pixel 
is a data example, so,in a picture with 128 x 128 there is 16284 pixel, and each pixel has a three - 8 bit integer representing the colors.
With k-means algorithm, we find a n(16-8-4,etc) color that best group(cluster) the pixels in the 3 dimensional RGB space.  
