This repository contains code of our CVPR 2021 paper - ["Learning Camera Localization via Dense Scene Matching"](https://arxiv.org/abs/2103.16792) by Shitao Tang, Chengzhou Tang, Rui Huang, Siyu Zhu and Ping Tan.

This paper presents a new method for scene agnostic camera localization using dense scene matching (DSM), where a cost volume is constructed between a query image and a scene. The cost volume and the corresponding coordinates are processed by a CNN to predict dense coordinates. Camera poses can then be solved by PnP algorithms.

If you find this project useful, please cite:
```
@inproceedings{Tang2021Learning,
  title={Learning Camera Localization via Dense Scene Matching},
  author={Shitao Tang, Chengzhou Tang, Rui Huang, Siyu Zhu and Ping Tan},
  booktitle={Computer Vision and Pattern Recognition (CVPR)},
  year={2021}
}
```

## Usage
### Environment
* The codes are tested along with 
  - pytorch=1.4.0
  - lmdb (optional)
  - yaml
  - skimage
  - opencv
  - numpy=1.17
  - tensorboard
### Installation
* Build PyTorch operations
  ```
    cd libs/model/ops
    python setup.py install
  ```
* Build PnP algorithm
  ```
    cd libs/utils/lm_pnp
    mkdir build
    cd build
    cmake ..
    make all
  ```
### Train and Test
* Download

  You can download the trained models and label files for [7scenes](https://drive.google.com/file/d/1XeLUsDuo3O4JgWEl1zLeht0kuy3E8kar/view?usp=sharing), [Cambridge](https://drive.google.com/file/d/1vshSXWt6dPG10Qg68yzhmpI_JLWcsjpk/view?usp=sharing), [Scannet](https://drive.google.com/file/d/1PVm67EjqqeHC59t-XqpGRKEr3EgGNzNc/view?usp=sharing).

  For 7scenes, you can use the prepared data in the following.

  |[Chess](https://drive.google.com/file/d/18PJHy-B3mcIaGW19GXv5H_RpesGYRg26/view?usp=sharing) |[Fire](https://drive.google.com/file/d/1sJMu8T9W78Lod5Bbei6I5IysumW1GWxc/view?usp=sharing) |[Heads](https://drive.google.com/file/d/1_8cqDvR5XLctt37JyGbbOy49m5pysb5v/view?usp=sharing) |[Office](https://drive.google.com/file/d/1dFvHmDjBWpyxIZNLzZ8JrsJoH6dFyRZm/view?usp=sharing) |[Pumpkin](https://drive.google.com/file/d/1N_5JPi31p9beR4VW7_T8f_131at2RGGN/view?usp=sharing) |[Kitchen](https://drive.google.com/file/d/1qlHoPYUzCyVhcG-GGGDIMFoBi7P_kfIo/view?usp=sharing) |[Stairs](https://drive.google.com/file/d/1xDObFp0fYeyJpEuW2aJKLok46UGOYwR3/view?usp=sharing) |
  |:-:|:-:|:-:|:-:|:-:|:-:|:-:|

  For Cambridge landmarks, you can download image files [here](http://mi.eng.cam.ac.uk/projects/relocalisation/), and depths [here](https://heidata.uni-heidelberg.de/api/access/datafile/:persistentId?persistentId=doi:10.11588/data/EGCMUU/7LBIQJ)

* Test
  
  Please refer to configs/7scenes.yaml for detailed explaination of how to set label file path and image file path 
  * 7scenes
    ```
    python tools/video_test.py --config configs/7scenes.yaml
    ```
  * Camrbrige
    ```
    python tools/video_test.py --config configs/cambridge.yaml
    ```

* Train

  We use ResNet-FPN pretrained [model](https://drive.google.com/file/d/1RpNR8J9lmI4S3yo5IPGlgMSva0lWBgMw/view?usp=sharing).
  ```
    python tools/train_net.py
  ```