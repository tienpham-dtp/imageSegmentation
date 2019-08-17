# imageSegmentation

In this problem, you will apply K-Means to image segmentation. Write a program named imageSegmentation.py that reads in an image, segments that image using K-Means clustering as described below, and outputs the new segmented image. Your program must support the following command line arguments:
           python imageSegmentation.py K inputImageFilename outputImageFilename
The first argument K is an integer greater than 2 that specifies the number of clusters, inputImageFilename is the filename of the input image, and outputImageFilename is the filename to write the output image. For example, we might call your program via:
           python imageSegmentation.py 24 newyorkcity.jpg nyc-segmented.jpg
           
           
[I chose a Van Gogh painting and my k = 5]

Choose several nice natural images, such as a farmhouse against a blue sky, or a city scene. First write code to load the image using the Python Image Library (you might find it useful to consult http://en. wikibooks.org/wiki/Python_Imaging_Library). The Python Image Library supports a wide variety of image file formats, and will automatically determine the filetype based on the file extension. (We will test your program with .jpg and .png files, so make certain to test your program with those types.)

We can think of an image as being represented as a 3-D matrix of size imageWidth × imageHeight × 3. For each location in the image (i, j), the matrix contains three values for the red, green, and blue components of the pixels. We will use these pixel values for clustering. In addition to the color values (rp,gp,bp) for pixel p, we will also use the x,y coordinates (ip,jp) as features. In particular, we can represent each pixel p as a five-dimensional data vector xp = 􏰄 rp gp bp ip jp 􏰅.

Complete the program via the following steps:
• Convert the input image into a data set with five features, as described above. To improve results, you should also standardize the values of each feature in the data set.
• Implement your own version of K-Means (don’t use the one built into sklearn) and use it to cluster the data (i.e. the features for each pixel) into K clusters. If a cluster is ever empty during the procedure, assign a random data point to it. Use random initializations for the cluster centers, and iterate until the centroids converge.
• Use the cluster centers to generate the segmented image by replacing each data point’s color values with the closest center. For example, xp becomes
xˆp =􏰄 rC(p) gC(p) bC(p) ip jp 􏰅 ,
where C(p) is the cluster to which xp belongs and (rC(p), gC(p), bC(p)) are the corresponding RGB values of that cluster’s centroid. Note specifically that we’re only replacing the color values of each instance
with its centroid’s colors, we’re not changing the (i,j) coordinates of that instance.
• Create an output image the same size as the input image. Then fill in the color values of each pixel of the image based on the xˆp’s. For example, xˆp informs us that the pixel at (ip,jp) should have color (rC(p),gC(p),bC(p)). Note that you also have to undo the feature standardization at this point (just invert the standardization equation by solving for the original value given the standardized value).
• Output the resulting image to the file outputImageFilename.
• In your writeup, include three different original images alongside the resulting segmented image.
The result of this process is called an over-segmented image. It is the first step to building such systems as
this: http://make3d.cs.cornell.edu/. Later steps would piece these segments together into objects.
