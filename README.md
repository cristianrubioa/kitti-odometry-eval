# kitti_odometry_eval

## Brief
[![C++: solutions](https://img.shields.io/badge/C++-Solutions-blue.svg?style=flat&logo=c%2B%2B)](https://es.wikipedia.org/wiki/C%2B%2B) [![support level: community](https://img.shields.io/badge/support%20level-community-lightgray.png)](http://wiki.ros.org/Industrial)

> KITTI odometry evaluation contains CPP files for loading estimated and ground truth poses, and then computing the following metrics: average translation error [%]
     & average rotation error [deg/m].


## Compile
The downloaded eval files can be compiled using c++ compiler (clang, c++, g++, mingw, etc.). I ran the following to compile on Linux:
```
g++ -O3 -DNDEBUG -o evaluate_odometry evaluate_odometry.cpp matrix.cpp
```

**Note:** To evaluate on the ground truth poses that we possess changed line [426](https://github.com/cristianrubioa/kitti_odometry_eval/blob/main/cpp/evaluate_odometry.cpp#L426) from:
``` for (int32_t i=0; i<11; i++) {```
to:
```
# PA poses available
for (int32_t i=PA; i<PA+1; i++) {

# Example -> poses available "05.txt, 06.txt"
for (int32_t i=5; i<7; i++) {
```

## Usage
To evaluate on the ground truth poses that possess. The compiled program (evaluate_odometry) can then be run:
```
/evaluate_odometry <result_sha>

# result_sha is the sub-directory containing the estimated poses
# poses must be in relative directory "results/<result_sha>/data"
# with each sequence as "XX.txt" inside the data folder

result_sha
├── data
│   └─── 00.txt
├── ...
└── ...

# Example
/evaluate_odometry 00
```

## Full Structure
Evaluation creates the following files:
- errors: space-delimited file with rows
     - first frame number
     - rotation error
     - translation error
     - sequence length (path length) [m]
     - speed [km/h]
- plot_error: Plots of error for each sequence
     - path length vs. rotation error
     - speed vs. rotation error
     - path length vs. translation error
     - speed vs. translation error
- plot_path: x and z coordinates [m] for the path of the ground truth and odometry output. The sequence start is also marked. Files are included that display coordinates of all points for each sequence.
- stats.txt: average translation error followed by average rotation error (i.e. comparing gt to gt yields 0.0 and 0.0...).

```
results
├──00 // * example <result_sha> 
│    ├── data
│    │   └─── 00.txt
│    ├── errors                   
│    │   └─── 00.txt
│    ├── plot_error               
│    │   └─── <pre_sub>.<format>      
│    │         // 1. <pre_sub> 
│    │         // 1.1 pre [avg, <num>] 
│    │         //      1.1.1 (avg: average, <num>:estimated pose)
│    │         // 1.2 sub [rl, rs, tl, ts] 
│    │         //      1.2.1 (r:rotation, t:translation, s:speed, l:path length)
│    │         // 2. <format> [ eps, gp, pdf, png, txt]
│    │         // 3. * example: avg_rl.pdf ... 00_rl.pdf ...                        
│    ├── plot path                                      
│    │   └─── 00.eps
│    │   └─── 00.gp
│    │   └─── 00.pdf
│    │   └─── 00.png
│    │   └─── 00.txt
│    stats.txt  
├── ...
└── ...
```  


## Reference
- [KITTI odometry development kit](http://www.cvlibs.net/datasets/kitti/eval_odometry.php) [Official devkit]
- [ORB-SLAM-Experiments-and-KITTI-Evaluation](http://edge.rit.edu/edge/C18501/public/ORB-SLAM-Experiments-and-KITTI-Evaluation_17006594.html)
