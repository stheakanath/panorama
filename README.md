# Panorama

Implementing Harris Interest Point Detector, Adaptive Non-Maximal Suppression, and RANSAC for automatic panorama stitching of multiple images.

![Panorama](http://i.imgur.com/iuiBMYs.png)

## Algorithm

We read in some images and then we extract the harris points from that. The harris function is given as harris(image, count, edge). Count is set to be 512 to be the maximum amount of points we want and edge is the filter of the gaussian blur. After we get the harris points of both images, we apply our ANMS algorithm, to filter the points down to about 150 points. 

The ANMS algorithm is given by the function anms(coords, top=400). anms takes in coords which is the coordinates of the feature points and their corner weights. and top is the maximum amount we want. This uses the helper function "distance" which calculates the distance between two points. After we surpress the points, we move on to getting extracting the descriptors of the image, given by the extract(img, harris, radius=8) function. extract takes the image, the harris points given by the previous functions and then the radius of our window we are looking at. 

Once we get the descriptors for each image, we pass this into matching(d1, d2), which matches the two points between the images. This returns the points that are matched.

After this we apply the RANSAC algorithm to select which points we want, after which we get a homogenous matrix. We then transform the images provided using this homogenous matrix and then stitch them together in the main function. The other functions not mentioned are just helper functions.

## Running Code
```
python main.py <Image 1> <Image 2>
```

Example with Images Provided:
``` 
python main.py Image1.jpg Image2.jpg
```
Outputted file is saved as image_processed.jpg in directory

