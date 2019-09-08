# SFND 2D Feature Tracking

<img src="images/keypoints.png" width="820" height="248" />

The idea of the camera course is to build a collision detection system - that's the overall goal for the Final Project. As a preparation for this, you will now build the feature tracking part and test various detector / descriptor combinations to see which ones perform best. This mid-term project consists of four parts:

* First, you will focus on loading images, setting up data structures and putting everything into a ring buffer to optimize memory load. 
* Then, you will integrate several keypoint detectors such as HARRIS, FAST, BRISK and SIFT and compare them with regard to number of keypoints and speed. 
* In the next part, you will then focus on descriptor extraction and matching using brute force and also the FLANN approach we discussed in the previous lesson. 
* In the last part, once the code framework is complete, you will test the various algorithms in different combinations and compare them with regard to some performance measures. 

See the classroom instruction and code comments for more details on each of these parts. Once you are finished with this project, the keypoint matching part will be set up and you can proceed to the next lesson, where the focus is on integrating Lidar points and on object detection using deep-learning. 

## Dependencies for Running Locally
* cmake >= 2.8
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1 (Linux, Mac), 3.81 (Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* OpenCV >= 4.1
  * This must be compiled from source using the `-D OPENCV_ENABLE_NONFREE=ON` cmake flag for testing the SIFT and SURF detectors.
  * The OpenCV 4.1.0 source code can be found [here](https://github.com/opencv/opencv/tree/4.1.0)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)

## Basic Build Instructions
1. Clone this repo.
2. Make a build directory in the top level directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./2D_feature_tracking`.


## Result

 |Detector|Descriptor|Matcher|#keypoint|time(detect)(ms)|#keypoint(vehicle)|time(descriptor)(ms)|#Matchedpoint(ms)|
|---|---|---|---|---|---|---|---|
|	SHITOMASI	|	BRISK	|	MAT_BF	|	1342.30	|	8.41	|	117.90	|	1.00	|	85.22	|
|	HARRIS	|	BRISK	|	MAT_BF	|	173.70	|	2.91	|	24.80	|	0.36	|	15.78	|
|	FAST	|	BRISK	|	MAT_BF	|	1787.40	|	0.47	|	149.10	|	1.16	|	99.89	|
|	BRISK	|	BRISK	|	MAT_BF	|	2711.40	|	23.77	|	276.30	|	1.90	|	174.44	|
|	ORB	|	BRISK	|	MAT_BF	|	500.00	|	3.93	|	116.10	|	0.90	|	83.44	|
|	AKAZE	|	BRISK	|	MAT_BF	|	1342.90	|	31.33	|	167.00	|	1.18	|	135.00	|
|	SIFT	|	BRISK	|	MAT_BF	|	1386.00	|	46.62	|	138.70	|	1.01	|	66.00	|
|	SHITOMASI	|	BRIEF	|	MAT_BF	|	1342.30	|	22.19	|	117.90	|	0.88	|	104.89	|
|	HARRIS	|	BRIEF	|	MAT_BF	|	173.70	|	4.49	|	24.80	|	0.23	|	19.22	|
|	FAST	|	BRIEF	|	MAT_BF	|	1787.40	|	0.50	|	149.10	|	0.51	|	122.11	|
|	BRISK	|	BRIEF	|	MAT_BF	|	2711.40	|	23.80	|	276.30	|	0.61	|	189.33	|
|	ORB	|	BRIEF	|	MAT_BF	|	500.00	|	4.03	|	116.10	|	0.37	|	60.56	|
|	AKAZE	|	BRIEF	|	MAT_BF	|	1342.90	|	31.29	|	167.00	|	0.48	|	140.67	|
|	SIFT	|	BRIEF	|	MAT_BF	|	1386.00	|	45.28	|	138.70	|	0.41	|	78.22	|
|	SHITOMASI	|	ORB	|	MAT_BF	|	1342.30	|	7.45	|	117.90	|	0.61	|	100.89	|
|	HARRIS	|	ORB	|	MAT_BF	|	173.70	|	2.93	|	24.80	|	0.54	|	18.00	|
|	FAST	|	ORB	|	MAT_BF	|	1787.40	|	0.47	|	149.10	|	0.65	|	119.00	|
|	BRISK	|	ORB	|	MAT_BF	|	2711.40	|	23.76	|	276.30	|	2.39	|	168.44	|
|	ORB	|	ORB	|	MAT_BF	|	500.00	|	3.95	|	116.10	|	2.50	|	84.78	|
|	AKAZE	|	ORB	|	MAT_BF	|	1342.90	|	31.35	|	167.00	|	1.54	|	131.33	|
|	SHITOMASI	|	FREAK	|	MAT_BF	|	1342.30	|	7.07	|	117.90	|	20.90	|	85.33	|
|	HARRIS	|	FREAK	|	MAT_BF	|	173.70	|	2.89	|	24.80	|	20.60	|	16.00	|
|	FAST	|	FREAK	|	MAT_BF	|	1787.40	|	0.47	|	149.10	|	21.38	|	97.56	|
|	BRISK	|	FREAK	|	MAT_BF	|	2711.40	|	23.68	|	276.30	|	21.57	|	169.33	|
|	ORB	|	FREAK	|	MAT_BF	|	500.00	|	4.38	|	116.10	|	21.68	|	46.67	|
|	AKAZE	|	FREAK	|	MAT_BF	|	1342.90	|	27.64	|	167.00	|	22.15	|	131.89	|
|	SIFT	|	FREAK	|	MAT_BF	|	1386.00	|	47.54	|	138.70	|	21.22	|	66.11	|
|	AKAZE	|	AKAZE	|	MAT_BF	|	1342.90	|	31.03	|	167.00	|	24.44	|	139.89	|
|	SHITOMASI	|	SIFT	|	MAT_FLANN	|	1342.30	|	8.33	|	117.90	|	7.59	|	103.22	|
|	HARRIS	|	SIFT	|	MAT_FLANN	|	173.70	|	2.94	|	24.80	|	8.15	|	18.11	|
|	FAST	|	SIFT	|	MAT_FLANN	|	1787.40	|	0.49	|	149.10	|	10.44	|	116.56	|
|	BRISK	|	SIFT	|	MAT_FLANN	|	2711.40	|	23.72	|	276.30	|	14.61	|	184.67	|
|	ORB	|	SIFT	|	MAT_FLANN	|	500.00	|	4.03	|	116.10	|	19.54	|	84.89	|
|	AKAZE	|	SIFT	|	MAT_FLANN	|	1342.90	|	32.17	|	167.00	|	10.13	|	141.78	|
|	SIFT	|	SIFT	|	MAT_FLANN	|	1386.00	|	46.46	|	138.70	|	38.43	|	89.22	|


## Performance evaluation
Number of keypoints rank:<br>
(detector)  BRISK(2711) > FAST(1787) > SIFT(1386) > AKAZE(1343) > SHITOMASI(1342) > ORB(500) > HARRIS(174) <br><br>
Percentage of matched kpts / kpts rank:<br>
<img src="images/percent_rank.png" width="977" height="910" /><br><br>

### the TOP3 detector / descriptor combinations: <br>
1. FAST/BRIEF: very fast, lots of keypoints, high matched percentage <br>
2. SHITOMASI/ORB: fast, many keypoints, high matched percentage<br>
3. SHITOMASI/SIFT: fast, many keypoints, high matched percentage<br>
