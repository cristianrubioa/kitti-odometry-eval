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
     ├──00.txt
├── ...
└── ...

# Example
/evaluate_odometry 00
```

## Full Structure

```
results
├──00 // * example <result_sha> 
    ├──data
        ├──00.txt
    ├──errors                   
        ├──00.txt
    ├──plot_error               
        ├──<pre_sub>.<format>      
           // 1. <pre_sub> 
           // 1.1 pre [avg, num_sequence] 
           // 1.2 sub [rl, rs, tl, ts] 
           //      1.2.1 (r:rotation, t:translation, s:speed, l:path length)
           // 2. <format> [pdf, png, eps, gp]
           // 3. * example: avg_rl.pdf ... 00_rl.pdf ...                        
    ├──plot path                                      
        ├──00.eps
        ├──00.gp
        ├──00.pdf
        ├──00.png
        ├──00.txt
    stats.txt                  
```  


## Reference
[KITTI odometry development kit](http://www.cvlibs.net/datasets/kitti/eval_odometry.php)
