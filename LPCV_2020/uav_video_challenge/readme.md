# Overview

This baseline OCR solution is a two step solution involving: 1) a text detection step, and 2) a text recognition step. The detection step (1), finds arbitrary rotated bounding boxes of text within a given image. It uses a Faster-RCNN detection architecture with a rotation RPN [1, 2]. The trunk is based on the dmasking model from the FBNet family for efficiency [3]. The recognition step (2) is run on image patches cropped from the original image to recognize single words from the bounding box. It is based on the character sequence encoding (CHAR) as proposed in [4] and trained in the Rosetta frame work [5]. The trunk is based on the fbnet_c model from the FBNet family for efficiency [3].

The models were trained with publicly available datasets. For the text detection mode, we use the SynthText in the Wild dataset [6]. The model was trained with detectron2go framework [7] with efficient model archs as specified [8]. For the text recognition model, we use data from both [6] and [9] for training. 

[1] J. Ma, W. Shao, H. Ye, L. Wang, H. Wang, Y. Zheng, and X. Xue. "Arbitrary-oriented scene text detection via rotation proposals",  in IEEE Trans. on Multimedia, 2018

[2] J. Huang, V. Sivakumar, M. Mnatsakanyan, and G. Pang. "Arbitrary-oriented scene text detection via rotation proposals",  arXiv preprint arXiv:1811.07031

[3] B. Wu, X. Dai, P. Zhang, Y. Wang, F. Sun, Y. Wu, Y. Tian, P. Vajda, Y. Jia, and K. Keutzer, “FBNet: Hardware-Aware Efficient ConvNet Design via Differentiable Neural Architecture Search”, in CVPR, 2019

[4] M. Jaderberg, K. Simonyan, A. Vedaldi, and A. Zisserman. “Synthetic Data and Artificial Neural Networks for Natural Scene Text Recognition”, in NeurIPS Deep Learning Workshop, 2014

[5] F. Borisyuk, A. Gordo, and V. Sivakumar. "Rosetta: Large scale system for text detection and recognition in images", in KDD, 2018

[6] A. Gupta, A. Vedaldi, and A. Zisserman, “Synthetic Data for Text Localisation in Natural Images”, in CVPR, 2016

[7] https://ai.facebook.com/blog/-detectron2-a-pytorch-based-modular-object-detection-library-/

[8] https://github.com/facebookresearch/mobile-vision/tree/master/mobile_cv/arch

[9] M. Jaderberg, K. Simonyan, A. Vedaldi, and A. Zisserman, “Reading Text in the Wild with Convolutional Neural Networks”, in IJCV, 2016

# Prerequisites

Sources depend on opencv, numpy, and pytorch. The model uses an RRPN that was not released with 1.4 so we need to link to nightly builds for requirements. Install dependencies as follows:

pip/pip3 install -r requirements.txt -f https://download.pytorch.org/whl/nightly/cpu/torch_nightly.html


# How to run

  python ./query_video.py --input_video <video file> --query_file <query text file> --config_file ./config.json

By default, it will run frame-by-frame which may be unnecessary for video files. You can change the run sampling rate by running as follows:

  python ./query_video.py --input_video <video file> --query_file <query text file> --config_file ./config.json --sampling_rate 10
