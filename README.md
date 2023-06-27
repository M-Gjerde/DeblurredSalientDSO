# DeblurredSalientDSO

DeblurredSalientDSO

## 1. What?
This is the accompanying source code for the paper **[DeblurredSalientDSO](https://ieeexplore.ieee.org)**

## 3. Citation
Cite the paper if it is usefull to you:

```
@ARTICLE{, 
author={}, 
journal={}, 
title={}, 
year={}, 
volume={}, 
number={}, 
pages={}, 
keywords={}, 
doi={}, 
ISSN={}, 
month={},}
```




Also, citing the original SalientDSO paper is appreciated.

```
@ARTICLE{salientdso, 
author={H. {Liang} and N. J. {Sanket} and C. {Fermüller} and Y. {Aloimonos}}, 
journal={IEEE Transactions on Automation Science and Engineering}, 
title={SalientDSO: Bringing Attention to Direct Sparse Odometry}, 
year={2019}, 
volume={}, 
number={}, 
pages={1-8}, 
keywords={Visualization;Semantics;Optimization;Task analysis;Cameras;Computer vision;Direct sparse odometry (DSO);scene parsing;SLAM;visual saliency.}, 
doi={10.1109/TASE.2019.2900980}, 
ISSN={}, 
month={},}
```

Also, citing the original DSO paper is appreciated.

```
@ARTICLE{dso, 
author={J. {Engel} and V. {Koltun} and D. {Cremers}}, 
journal={IEEE Transactions on Pattern Analysis and Machine Intelligence}, 
title={Direct Sparse Odometry}, 
year={2018}, 
volume={40}, 
number={3}, 
pages={611-625}, 
keywords={distance measurement;image motion analysis;image sampling;optimisation;probability;direct sparse odometry;visual odometry method;motion formulation;fully direct probabilistic model;consistent optimization;joint optimization;reference frame;camera motion;sample pixels;smooth intensity variations;Cameras;Geometry;Three-dimensional displays;Optimization;Robustness;Computational modeling;Visualization;Visual odometry, SLAM, 3D reconstruction, structure from motion}, 
doi={10.1109/TPAMI.2017.2658577}, 
ISSN={}, 
month={March},}
```

## 4. Setup Instructions

#### 4.1 Prerequisites
Follow prerequisites for the [SalientDSO](https://github.com/prgumd/SalientDSO) 

#### 4.2.2. Building
Compile as:
```
cd DeblurredSalientDSO
mkdir build
cd build
cmake ..
make -j4

```



this will compile a library ```libdso.a```, which can be linked from external projects. It will also build a binary dso\_dataset, to run SalientDSO on datasets. Once you've tested this you can re-compile using ```USE_SALIENCY_SAMPLING=true``` in ```setting.h``` to use SalientDSO functionality.


### 5. Usage


#### 5.1. Test Deblurred Semantic Filtered Saliency Setting (SalientDSO's proposed approach)
Recompile using ```USE_SALIENCY_SAMPLING=true``` in ```setting.h``` to use this functionality. 
```
DATASETPATH=Path to your dataset
build/bin/dso_dataset files=DATASETPATH/images.zip calib=DATASETPATH/camera.txt gamma=DATASETPATH/pcalib.txt vignette=DATASETPATH/vignette.png saliency=DATASETPATH/saliency/ segmentation=DATASETPATH/segmentation/ preset=0 mode=0 smoothing=2  \ 
useDeblur=on

```

### Additional Dataset Format
The format assumed is that of [https://vision.in.tum.de/mono-dataset](https://vision.in.tum.de/mono-dataset).
However, it should be easy to adapt it to your needs, if required. The binary is run with:

- `saliency=XXX` where XXX is either a folder or .zip archive containing saliency images. They are sorted *alphabetically*. for .zip to work, need to comiple with ziplib support.

- `segmentation=XXX` where XXX is either a folder or .zip archive containing saliency images. They are sorted *alphabetically*. for .zip to work, need to comiple with ziplib support.

- `calib_no_rect=XXX` where XXX is a geometric camera calibration file. It is used if saliency images and segmentations is already undistorted.

### Commandline Options
there are many command line options available, see `main_dso_pangolin.cpp`. some examples include
- `result=XXX` : set the path to the output trajectory file
- `smoothing=X` : 
  -`smoothing=0` : set saliency smoothing term to a constant
  -`smoothing=1` : set saliency smoothing term to the average of the saliency / saliencyMeanWeight
  -`smoothing=2` : apply saliency filtering and set saliency smoothing term to a constant
- `saliencyAdd=X` : set constant term for saliency smoothing to X
- `immatureDensity=X` : set the number of candidate points to X
- `saliencyMeanWeight=X` : set saliencyMeanWeight for saliency smoothing to X
- `patchSize=X` : set the size KxK of sampling patch to XxX
- `points=XXX` : set the path to the output 3D point cloud(sampleoutput has to be set to 1)



## 7. Acknowledgments

We would like to thank the authors of [DSO](https://github.com/JakobEngel/dso) and [SalientDSO](https://github.com/prgumd/SalientDSO) on which this code is based on.
