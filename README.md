# kitti_odometry_eval
KITTI odometry evaluation

## Compile
The downloaded eval files can be compiled using c++ compiler (clang, c++, g++, mingw, etc.). I ran the following to compile on Linux:
```
g++ -O3 -DNDEBUG -o evaluate_odometry evaluate_odometry.cpp matrix.cpp
```

To evaluate on the ground truth poses that we possess changed line [426](https://github.com/cristianrubioa/kitti_odometry_eval/blob/main/cpp/evaluate_odometry.cpp#L426) from:
``` for (int32_t i=0; i<11; i++) {```
to:
```
# PA pose available
for (int32_t i=PA; i<PA+1; i++) {

# Example -> pose available "05.txt"
for (int32_t i=5; i<6; i++) {
```

## Usage
To evaluate on the ground truth poses that possess. The compiled program (evaluate_odometry) can then be run:
```
/evaluate_odometry RESULT_PATH

# RESULT_PATH contains the pose text file, 
# which should be named as 00.txt, 01.txt, ...
# inside the data folder data

RESULT_PATH
├── data
  ├──00.txt
├── ...
└── ...

# Example
/evaluate_odometry 00
```

## Full Structure

```
results
├──00
  ├──data
    ├──00.txt
  ├──errors
    ├──00.txt
  ├──plot_error
    ├──05_rl.pdf
    ├──05_rs.pdf
    ├──05_tl.pdf
    ├──05_ts.pdf
    ├──avg_rl.pdf
    ├──avg_rs.pdf
    ├──avg_tl.pdf
    ├──avg_ts.pdf
    ...
  ├──plot path
    ├──00.eps
    ├──00.gp
    ├──00.pdf
    ├──00.png
```  


## Reference
[KITTI odometry development kit](http://www.cvlibs.net/datasets/kitti/eval_odometry.php)
