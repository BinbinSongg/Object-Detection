# Object-Detection
# Theory: 
Now, how do we actually go about this process? So when you want to build a Haar Cascade, you need "positive" images, and "negative" images. The "positive" images are images that contain the object you want to find. This can either be images that just mainly have the object, or it can be images that contain the object, and you specify the ROI (region of interest) where the object is. With these positives, we build a vector file that is basically all of these positives put together. One nice thing about the positives is that you can actually just have one image of the object you wish to detect, and then have a few thousand negative images. Yes, a few thousand. The negative images can be anything, except they cannot contain your object.

Example: 
Detect everything based on OpenCV

opencv_createsamples (only one positive image)
create a bunch of positive examples, using your negative images. 
(for more positive images – download from “imageNet” or other websites) – better server (50000 positive, 2500 negative)

# Step1: 
Take a photo as the positive image (50 x 50 size), and 
download negative images online, from website “imageNet”

make them (negative images) become same size (100 x 100) from “face.py”

# Step2: 
Filter out some bad pictures by function in “face.py”

# Step3:
Create negative samples 
Create the path for each negative image 
Use opencv_createsamples (commands below)

# Step4: train the classifier

create two files 
mkdir data
mkdir info 

create new positive examples 
<opencv_createsamples –image pos.jpg> --- positive image 
-bg bg.txt ---image path (the algorithm can find it)
-info info/info.lst ---store all the information about new positive images, like bg.txt
-pngoutput info ---where to put the output image 
-maxxangle 0.5 the angle of original positive image 
-maxyangle -0.5 
-maxzangle 0.5 
-num 1950 –how many output. 

Together- 
opencv_createsamples -img pos.jpg -bg bg.txt -info info/info.lst -pngoutput info -maxxangle 0.5 -maxyangle -0.5 -maxzangle 0.5 -num 1950

# step4 (create vector file): 
together:
opencv_createsamples -info info/info.lst -num 1950 -w 20 -h 20 -vec positives.vec 

20 x 20, larger, computational expensive.---longer time. 
Haar cascades will find some small featuers—so it is not need to use large size

# Step5: 
(train the algorithm):
opencv_traincascade -data data -vec positives.vec -bg bg.txt -numPos 1800 -numNeg 900 -numStages 15 -w 20 -h 20

-data , where to put output .xml file 
-vec, the vec file set before 
-bg bg.txt , background file 
-numPos 1800 don't make it too large, it will increase stage by stage 
- numNeg half of positive images 
- w 20
- h 20 


Errors：
Insufficient count of samples in given vec-file. 
Solutions: reduce initial numPos; or create more negative samples and increase vec-file. 

