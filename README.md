# Light field super-resolution by jointly exploiting internal and external similarities

**Official implementation** for the following paper

Zhen Cheng, Zhiwei Xiong*, Dong Liu, "[Light field super-resolution by jointly exploiting internal and external similarities](https://ieeexplore.ieee.org/document/8733069)", IEEE Transactions on Circuits and Systems for Video Technology (T-CSVT), In press.

## Requirements
- Caffe 1.0
- CUDA and Cudnn suited for Caffe 1.0
- MATLAB with pre-compiled matcaffe
## Usage

Our framework consists of 6 main procedures: **PRO-IB** [4], **VDSR** [1], **disparity estimation** [3], **warp**, **EnhanceCNN** and **FusNet**. 

In this repo, we provide the trained models and the network configurations for VDSR, EnhanceCNN, and FusNet, repectively. The other procedures can be reproduced by using official projects or our re-implementation codes.

### PRO-IB

PRO-IB is the advanced projection-based light field SR algorithm. We've released the re-implmentation codes. Please refer to [code for PRO](https://github.com/Joechann0831/LFSRBenchmark/tree/master/PRO) for detailed information.

### VDSR

VDSR is originally designed for single image SR [1]. We adopte the pre-trained weights of VDSR for initialization, which generates the HR inputs of EnhanceCNN. We re-train the network for Gaussian downsampling at a scale factor of 3 using the same dataset as in [1]. Please refer to [our re-implementation of VDSR with Caffe](https://github.com/Joechann0831/LFSRBenchmark/tree/master/VDSR) for detailed information.

### disparity estimation

Disparity estimation is an important procedure in our framework, since the estimated disparity map will be used for both PRO-IB and EnhanceCNN. We adopt the state-of-the-art method proposed in [3] for disparity estimation. The official code can be found at [http://cseweb.ucsd.edu/~viscomp/projects/LF/papers/ICCV15/occCode.zip](http://cseweb.ucsd.edu/~viscomp/projects/LF/papers/ICCV15/occCode.zip).

### warp

The warp operation is used to align the reference view to the target view using the disparity map between them. If you want to implement it using MATLAB, you can refer to the MATLAB function *interp2*. If you want it as a Caffe layer (i.e., implemented with CUDA), you can refer to the code of [FlowNet](http://lmb.informatik.uni-freiburg.de//Publications/2017/IMKDB17) or [LFVcode](http://cseweb.ucsd.edu/~viscomp/projects/LF/papers/SIG17/lfv/). Note that our framework is not end-to-end, so it's not necessary to implement the warp operation using Caffe.

### EnhanceCNN and FusNet

We provide the trained model parameters and the network configuration files of EnhanceCNN and FusNet in this repo. The parameters are trained on EPFL dataset [2].

## Reference

[1] J. Kim, J. Kwon Lee, and K. Mu Lee. Accurate image super-resolution using very deep convolutional networks. In CVPR, 2016.

[2] M. Rerabek and T. Ebrahimi. New light field image dataset. In International Conference on Quality of Multimedia Experience (QoMEX), 2016.

[3] T. C. Wang, A. A. Efros, and R. Ramamoorthi. Occlusion-aware depth estimation using light-field cameras. In ICCV, 2015.

[4] C.-K. Liang and R. Ramamoorthi. A light transport framework for lenslet light field cameras. ACM Transactions on Graphics, 34(2):16:1-16:19, 2015.
