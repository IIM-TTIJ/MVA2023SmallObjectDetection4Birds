# MVA2023 - Small Object Detection for Birds Challenge 

<img src="http://www.mva-org.jp/mva2023/data/uploads/bird/samples-1.pdf.jpg" alt="mva-sod4b-sample" title="mva2023-ChallengeOnSmallObjectDetection4Birds-sample">


This repository includes the baseline code used in our [challenge](http://www.mva-org.jp/mva2023/challenge) .
It is built on MMDetection V2.24.1 (released on Apr 30, 2022, source code is downloaded from [here](https://github.com/open-mmlab/mmdetection/releases/tag/v2.24.1)).


### Important dates
|  Challenges Event  |  Date (always 23:59 PST)  |
| ---- | ---- |
| [Site online](http://www.mva-org.jp/mva2023/challenge) | 2022.12.8 |
| Release of training data and public test data | 2023.1.9 |
| Public test server online | 2023.1.10 |
| Public test server closed | 2023.4.14 |
| Fact sheets, code/executable submission deadline | 2023.4.21 |
| Paper submission deadline (only Research Category) | 2023.5.7 |
| Preliminary private test results release to the participants | 2023.6.15 |
| Camera ready due (only Research Category) | 2023.7.4 |

## News
[2023/01/10] Released dataset   
[2022/12/29] Important dates, Links and References are available.  


## Dataset
**[Download Link](https://drive.google.com/drive/folders/1vTHiIelagbzPO795yhOdNUFh9u2XxZP-?usp=share_link)**  

Dataset Directory Structure
```
data
 ├ drone2021
 │  ├ images
 │  └ annotations
 ├ mva2023_sod4bird_train
 │  ├ images
 │  └ annotations
 ├ mva2023_sod4bird_pub_test
 │  ├ images
 │  └ annotations(including an empty annotation file)
 └ mva2023_sod4bird_private_test
    ├ images(empty)
    └ annotations(empty)
```

The dataset is split into training / public test / private test sets. Participants can download the images and annotations of the training data, and the images of the public test data. The annotations of the public test data are hidden but the participants can obtain the evaluation score once their detection results are online submitted via the [**CodaLab web platform**](https://codalab.lisn.upsaclay.fr/competitions/9594). Participants cannot access the private test images. The private test will be conducted manually by the challenge organizer. The trainig data includes an extended version of the publicly available data (train1) published in [4] and newly released data for this competition (train2).
* Images and instances:
    * Train :
        * Train1(modified based on [[2]](https://github.com/kakitamedia/drone_dataset)) (drone2021): Consists of approximately 48,395 images with about 62,106 annotated bird instances.
        * Train2 (mva2023_sod4bird_train): Consists of approximately 9,759 images with about 29,037 annotated bird instances.
    * Public test (mva2023_sod4bird_pub_test) : Consists of approximately 9,699 images with about 29,775 annotated bird instances.
    * Private test (mva2023_sod4bird_private_test): Consists of approximately 10,000 images with about 30,000 annotated bird instances.
* Data format :
    * Input : Image
    * Annotation : COCO format

After the challenge, the public test evaluation server will continue to run on CodaLab to promote further research on small object detection.


## Links
* [MVA Official Competition Site](http://www.mva-org.jp/mva2023/challenge)
* [CodaLab](https://codalab.lisn.upsaclay.fr/competitions/9594)
* [Competiton train and public test Dataset Download Link](https://drive.google.com/drive/folders/1vTHiIelagbzPO795yhOdNUFh9u2XxZP-?usp=share_link)

## Citation

```
@misc{sodbchallenge2023misc,
title={Small Object Detection for Birds Challenge 2023},
author={Yuki Kondo, Norimichi Ukita},
howpublished={\url{https://www.mva-org.jp/mva2023/SODchallenge}},
year={2023}}

@inproceedings{sodbchallenge2023},
title={Small Object Detection for Birds Challenge 2023},
author={Yuki Kondo, Norimichi Ukita, [Winners]},
booktitle={International Conference on Machine Vision and Applications},
note={\url{https://www.mva-org.jp/mva2023/SODchallenge}},
year={2023}}

```


## About baseline code

This code was created with reference to MMDetection[3]. 
OpenMMLab provides a [Colab tutorial](https://github.com/open-mmlab/mmdetection/blob/master/demo/MMDet_Tutorial.ipynb).
If you are not familiar with MMDetection, please read its [tutorial](https://mmdetection.readthedocs.io/en/stable/) for how to modify the baseline code (e.g., replacing the detectors, backbones, learning rate, dataset and other hyperparameters in config files).
### Installation

We follow the [MMDetection Installation Website](https://github.com/open-mmlab/mmdetection/blob/master/docs/en/get_started.md/#Installation)
to install mmdet.

**Step 0.** Create a conda environment and activate it.

```shell
conda create -n mva python=3.7
conda activate mva
```

**Step 1.** Install PyTorch following [official instructions](https://pytorch.org/get-started/locally/)

We tested our code on `pytorch-1.10.2` and `pytorch-1.12.1`, please feel free to use other PyTorch versions.


**Step 2.** Install [MMCV](https://github.com/open-mmlab/mmcv) using [MIM](https://github.com/open-mmlab/mim).

```shell
pip install -U openmim
mim install mmcv-full
```
**Step 3.** Install our baseline code
```shell
git clone https://github.com/IIM-TTIJ/MVA2023SmallObjectDetection4Birds.git
cd MVA2023BirdDetection
pip install -v -e .
```


### Dataset 
**[Download Link](https://drive.google.com/drive/folders/1vTHiIelagbzPO795yhOdNUFh9u2XxZP-?usp=share_link)**  
Please put it at `data/` after you download and uncompress it.

Directory Structure
```
data
 ├ drone2021
 ├ mva2023_sod4bird_train
 ├ mva2023_sod4bird_pub_test
 └ mva2023_sod4bird_private_test
```



### Evaluation metrics
The evaluation in this repository is based on COCO mAP.  
The [COCO API[4]](https://github.com/cocodataset/cocoapi) is used to evaluate the detection results.
The evaluation of the [MVA2023 Challenge on Small Bird Detection competition](http://www.mva-org.jp/mva2023/challenge) is based on AP0.5.
We think that using the official COCO mAP is good for developing your method as metrics such as AP0.5, AP0.75, AP_samll 
are also reported, so we keep it here.


### Commands to run the code

We used CenterNet (backbone ResNet18) in the baseline and obtained mAP 47.3.
With hard negative training for additional 20 epochs, mAP was improved to 51.0. 

We have prepared the commands for conducting the distributed training and test in [`dist_train_test.sh`](dist_train_test.sh).


```shell
#!/usr/bin/env bash
export TORCH_DISTRIBUTED_DEBUG=INFO 
export CUDA_VISIBLE_DEVICES=0,1
export OMP_NUM_THREADS=1
export MKL_NUM_THREADS=1
GPU_NUM=2

###############################
# Step 1: normal training on data/drone2021
###############################
bash tools/dist_train.sh  configs/mva2023_baseline/centernet_resnet18_140e_coco.py $GPU_NUM


###############################
# Step 2: Generate predictions on data/drone2021 to select hard negatives examples
###############################
CONFIG=configs/mva2023_baseline/centernet_resnet18_140e_coco_inference.py
CHECKPOINT=work_dirs/centernet_resnet18_140e_coco/latest.pth
NNODES=${NNODES:-1}
NODE_RANK=${NODE_RANK:-0}
PORT=${PORT:-29501}
MASTER_ADDR=${MASTER_ADDR:-"127.0.0.1"}

python -m torch.distributed.launch \
    --nnodes=$NNODES \
    --node_rank=$NODE_RANK \
    --master_addr=$MASTER_ADDR \
    --nproc_per_node=$GPU_NUM \
    --master_port=$PORT \
 tti/test.py \
    --config $CONFIG \
    --checkpoint $CHECKPOINT \
    --launcher pytorch \
    --generate-hard-negative-samples True \
    --hard-negative-file work_dirs/centernet_resnet18_140e_coco/train_coco_hard_negative.json \
    --hard-negative-config 'num_max_det=10, pos_iou_thr=1e-5, score_thd=0.05, nms_thd=0.05'
    
# The setting for 'hard-negative-config' is the default setting for generating the hard negative examples. Please feel free to modify it.
# --------------------------


###############################
# Step 3: Hard negative training  on data/drone2021
###############################
bash tools/dist_train.sh  configs/mva2023_baseline/centernet_resnet18_140e_coco_hard_negative_training.py $GPU_NUM


###############################
# Step 4:fine-tuning on data/mva2023_sod4bird_train
###############################
bash tools/dist_train.sh  configs/mva2023_baseline/centernet_resnet18_140e_coco_finetune.py $GPU_NUM


###############################
# Step 5: To generate the predictions for submission
###############################
bash tools/dist_test.sh \
    configs/mva2023_baseline/centernet_resnet18_140e_coco_finetune.py \
    work_dirs/centernet_resnet18_140e_coco_finetune/latest.pth \
    2 \ 
    --format-only \
    --eval-options jsonfile_prefix=results

_time=`date +%Y%m%d%H%M`
mv results.bbox.json `submit/results_${_time}.json`
zip "submit/submit_${_time}.zip" `submit/results_${_time}.json`

```

To submit your detection result, first rename your resulting file to `results.json` so that
our Server can automatically evaluate your submission (other name is not acceptable), then compress your `results.json` to a zip file (any name is OK, e.g., submit.zip). A sample submission file is provided at `submit/public_test_smaple_submission.zip`. 


## References
[1] Hank Chen, Awesome Tiny Object Detection, https://github.com/kuanhungchen/awesome-tiny-object-detection  
[2] Fujii, Sanae, Kazutoshi Akita, and Norimichi Ukita. "Distant Bird Detection for Safe Drone Flight and Its Dataset." 2021 17th International Conference on Machine Vision and Applications (MVA). IEEE, 2021. https://github.com/kakitamedia/drone_dataset   
[3] Chen, Kai, et al. "MMDetection: Open mmlab detection toolbox and benchmark." arXiv preprint arXiv:1906.07155 (2019). https://github.com/open-mmlab/mmdetection  
[4] Piotr Dollar and Tsung-Yi Lin, COCO API, https://github.com/cocodataset/cocoapi  
