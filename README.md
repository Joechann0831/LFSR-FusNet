# Light field super-resolution by jointly exploiting internal and external similarities

**Official implementation** for the following paper

Zhen Cheng, Zhiwei Xiong*, Dong Liu, "[Light field super-resolution by jointly exploiting internal and external similarities](https://ieeexplore.ieee.org/document/8733069)", IEEE Transactions on Circuits and Systems for Video Technology (T-CSVT), In press.

## Requirements
- Caffe 1.0
- CUDA and Cudnn suited for Caffe 1.0
- MATLAB with pre-compiled matcaffe
## Usage

Our framework consists of 6 main procedures: **PRO-IB**, **VDSR** [1], **disparity estimation**, **warp**, **EnhanceCNN** and **FusNet**. 

In this repo, we provide the model parameters of VDSR, EnhanceCNN and FusNet trained with EPFL dataset [2]. For testing and training, we also provide the network configuration file with format of *.prototxt*.

### PRO-IB

PRO-IB is the advanced projection-based light field SR algorithm, we've already release the code.  Please refer to [code for PRO](https://github.com/Joechann0831/LFSRBenchmark/tree/master/PRO) for usage.

### VDSR

VDSR is used for initializing the HR inputs for EnhanceCNN. We re-train the network for Gaussian downsampling with scale 3 using the same dataset as in [1]. For complete training and testing codes, please refer to [Our re-implementation of VDSR with Caffe](https://github.com/Joechann0831/LFSRBenchmark/tree/master/VDSR).

### disparity estimation

Disparity estimation is an important procedure in our framework cause the estimated disparity map will be used for both PRO-IB and EnhanceCNN. We adopt the state-of-the-art method proposed in [3], the official code can be find at [http://cseweb.ucsd.edu/~viscomp/projects/LF/papers/ICCV15/occCode.zip](http://cseweb.ucsd.edu/~viscomp/projects/LF/papers/ICCV15/occCode.zip).

### warp

The operation warp is used to align reference view to the target view using the disparity map between them. If you want to implement it using MATLAB, you can refer to the MATLAB function *interp2*. If you want it as a Caffe layer (implemented with CUDA), you can refer to the code of [FlowNet](http://lmb.informatik.uni-freiburg.de//Publications/2017/IMKDB17) or [LFVcode](http://cseweb.ucsd.edu/~viscomp/projects/LF/papers/SIG17/lfv/). Note that our framework is not end-to-end, so it's not necessary to implement the warp operation using Caffe.

### EnhanceCNN and FusNet

We provide the trained model parameters and the network configuration files of EnhanceCNN and FusNet here. The parameters are trained with EPFL dataset [2].

## Reference

[1] J. Kim, J. Kwon Lee, and K. Mu Lee. Accurate image super-resolution using very deep convolutional networks. In CVPR, 2016.

[2] M. Rerabek and T. Ebrahimi. New light field image dataset. In International Conference on Quality of Multimedia Experience (QoMEX), 2016.

[3] T. C. Wang, A. A. Efros, and R. Ramamoorthi. Occlusion-aware depth estimation using light-field cameras. In ICCV, 2015.

