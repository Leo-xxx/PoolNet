## A Simple Pooling-Based Design for Real-Time Salient Object Detection

### This is a PyTorch implementation of our CVPR 2019 [paper](https://arxiv.org/abs/1904.09569).

## Prerequisites

- [Pytorch 0.4.1+](http://pytorch.org/)
- [torchvision](http://pytorch.org/)

## Usage

### 1. Clone the repository

```shell
git clone https://github.com/backseason/PoolNet.git
cd PoolNet/
```

### 2. Download the dataset

Download the following datasets and unzip them into `data` folder.

* [MSRA-B and HKU-IS](https://drive.google.com/open?id=1immMDAPC9Eb2KCtGi6AdfvXvQJnSkHHo) dataset. The .lst file for training is `data/msrab_hkuis/msrab_hkuis_train_no_small.lst`.
* [DUTS](https://drive.google.com/open?id=14RA-qr7JxU6iljLv6PbWUCQG0AJsEgmd) dataset. The .lst file for training is `data/DUTS/DUTS-TR/train_pair.lst`.

### 3. Download the pre-trained models


Download the following [pre-trained models](https://drive.google.com/open?id=1Q2Fg2KZV8AzNdWNjNgcavffKJBChdBgy) into `data/pretrained` folder. (Now we only provide models trained w/o edge)

### 5. Train

1. Set the `root` and `source` path in the `dataset/dataset.py` correctly.

2. We demo using ResNet-50 as network backbone and train with a initial lr of 5e-5 for 24 epoches, which is divided by 10 after 15 epochs.
```shell
python main_1task.py --arch resnet # you can optionly change the -lr and -wd params
```

3. After training the result model will be stored under `results/run-*` folder.

### 6. Test

For single dataset testing: `*` changes accordingly and `--sal_mode` indicates different datasets (details can be found in `dataset/dataset.py`)
```shell
python main.py --mode='test' --model='results/run-*/models/final.pth' --test_fold='results/run-*-sal-e' --sal_mode='e'
```
For all datasets testing used in our paper: `2` indicates the gpu to use
```shell
./forward.sh 2 main.py results/run-*
```

All results saliency maps will be stored under `results/run-*-sal-*` folders in .png formats.


### 7. Pre-trained models, pre-computed results and evaluation results

We provide the pre-trained model, pre-computed saliency maps and evaluation results of our PoolNet-ResNet50 w/o edge model [run-0](https://drive.google.com/open?id=12Zgth_CP_kZPdXwnBJOu4gcTyVgV2Nof).


Note：

1. only support `bath_size=1`


### If you think this work is helpful, please cite
```latex
@inproceedings{Liu2019PoolSal,
  title={A Simple Pooling-Based Design for Real-Time Salient Object Detection},
  author={Jiang-Jiang Liu and Qibin Hou and Ming-Ming Cheng and Jiashi Feng and Jianmin Jiang},
  booktitle={IEEE CVPR},
  year={2019},
}
```
```latex
@article{hou2019deeply,
  title={Deeply Supervised Salient Object Detection with Short Connections.},
  author={Hou, Qibin and Cheng, Ming-Ming and Hu, Xiaowei and Borji, Ali and Tu, Zhuowen and Torr, Philip HS},
  journal={IEEE transactions on pattern analysis and machine intelligence},
  year={2019}
}
```

Thanks to [DSS](https://github.com/Andrew-Qibin/DSS) and [DSS-pytorch](https://github.com/AceCoooool/DSS-pytorch).