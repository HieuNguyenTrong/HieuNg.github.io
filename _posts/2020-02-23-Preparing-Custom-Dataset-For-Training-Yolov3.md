**Created: 2020-Feb-23**
**By: Jason Ng**


# Collecting dataset and annotating/labeling as below:


## Gathering data by Google Image Search from a chrome extenion callsed Download All Images through a **zip** icon of Google Chrome.

[https://chrome.google.com/webstore/detail/download-all-images/ifipmflagepipjokmbdecpmjbibjnakm?hl=en%22]


## Labeling Data

Labeling means drawing bounding boxes around the objects:
Installing a tool **LabelImg** as below:

> pip install labelimg

Once **labelImg** is successfully installed, launch it by typing.


## After all the images are loaded, we can start labeling the images.

Convert to .JPEG from any type of images.
> mogrify -format jpg *.JPEG or mogrify -format jpg *.jpeg or mogrify -format jpg *.png 

Change the annotation format to **YOLO** from **PASCAL VOC** on the left panel before proceeding.

> labelImg [path to image] [classes file]


```
[path to image] is the path to an image in the directory containing the downloaded images we are going to label.

[classes file] is the file where we list the object classes that we are going to label..

For example: 

labelImg /home/Downloads/drone_images/drone_image_0.jpg classes.txt 

With classes.txt has one class: drone

```


**Keyboard shortcuts**

**W** 			- to start creating bounding box

**Ctrl + S** 		- to save the bounding boxes and labels

**D** 			- next image

**A**			- previous image


**YOLO format**

*object-id center_x center_y width height*

*object-id* represents the number corresponding to the object category which listed in **classes.txt** earlier.

*center_x and center_y* represents the center point of the bounding box. But they are normalized to range between 0 and 1 by dividing by the width and height of the image.

```
For example, (0.25,0.75) is the point located at 25% of the width and 75% of the height.
We can multiply this number (0.25,0.75) by the original width and height of the image to get the real point. 
In fact, we will be doing this at the end after inference to draw the predictions on the image.
Generally it is easier for the network to predict values between 0 and 1 than random coordinate values.
```
*width and height* represents the width and height of the bounding box. Again normalized to the range 0 to 1 dividing by the original width and height of the image.

