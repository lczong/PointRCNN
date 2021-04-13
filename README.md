# Point RCNN for HSD

## 环境配置

### Requirements

* Linux (Ubuntu 18.04)
* Python 3.6+
* PyTorch 1.0

### Installation

1. 克隆仓库

``` shell
git clone --recursive https://github.com/lczong/PointRCNN.git
```

2. pip安装依赖库

``` shell
pip install easydict tqdm tensorboardX shapely
```

3. 编译安装 `pointnet2_lib`, `iou3d`, `roipool3d` 库

``` shell
sh build_and_install.sh
```

## 数据集准备

KITTI文件夹放入数据集，注意要新建object文件夹，这里不加入planes

```
PointRCNN
├── data
│   ├── KITTI
│   │   ├── ImageSets
│   │   ├── object
│   │   │   ├──training
│   │   │      ├──calib & velodyne & label_2 & image_2
│   │   │   ├──testing
│   │   │      ├──calib & velodyne & image_2
├── lib
├── pointnet2_lib
├── tools
```

## Training

生成 ground truth database

``` shell
python generate_gt_database.py --class_name 'Car' --split train
```

### Training of RPN stage

``` shell
python train_rcnn.py --cfg_file cfgs/default.yaml --batch_size 16 --train_mode rpn --epochs 200
```

