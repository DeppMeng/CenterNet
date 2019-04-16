# CenterNet
## Getting Started
Please first install [Anaconda](https://anaconda.org) and create an Anaconda environment using the provided package list.
```
conda create --name CenterNet --file conda_packagelist.txt
```

After you create the environment, activate it.
```
source activate CenterNet
```

### Compiling Corner Pooling Layers
```
cd <CenterNet dir>/models/py_utils/_cpools/
python setup.py install --user
```

### Compiling NMS
cd <CenterNet dir>/external
make
```

### Installing MS COCO APIs
```
cd <CenterNet dir>/data/coco/PythonAPI
make
```

### Downloading MS COCO Data
- Download the training/validation split we use in our paper from [here](https://drive.google.com/file/d/1dop4188xo5lXDkGtOZUzy2SHOD_COXz4/view?usp=sharing) (originally from [Faster R-CNN](https://github.com/rbgirshick/py-faster-rcnn/tree/master/data))
- Unzip the file and place `annotations` under `<CenterNet dir>/data/coco`
- Download the images (2014 Train, 2014 Val, 2017 Test) from [here](http://cocodataset.org/#download)
- Create 3 directories, `trainval2014`, `minival2014` and `testdev2017`, under `<CenterNet dir>/data/coco/images/`
- Copy the training/validation/testing images to the corresponding directories according to the annotation files

## Training and Evaluation

To train CenterNet-104:
```
python train.py CenterNet-104
```
We provide the configuration file (`CenterNet-104.json`) and the model file (`CenterNet-104.py`) for CenterNet in this repo. 

We also provide a trained model for `CenterNet-104`, which is trained for 480k iterations using 8 Tesla V100 (32GB) GPUs. You can download it from [here](https://pan.baidu.com/s/17RvbWaxrvW1kXRuk7XmIfw  code:2clj) and put it under `<CenterNet dir>/cache/nnet`. If you want to train you own CenterNet, please adjust the batch size in `CenterNet-104.json` to accommodate the number of GPUs that are available to you.

To use the trained model:
```
python test.py CenterNet-104 --testiter 480000 --split <split>
```

To train CenterNet-52:
```
python train.py CenterNet-52
```
We provide the configuration file (`CenterNet-52.json`) and the model file (`CenterNet-52.py`) for CenterNet in this repo. 

We also provide a trained model for `CenterNet-52`, which is trained for 480k iterations using 8 Tesla V100 (32GB) GPUs. You can download it from [here](https://pan.baidu.com/s/1Ltig0csUPp4T5HA4BjHikA  code:ed0y) and put it under `<CenterNet dir>/cache/nnet`. If you want to train you own CenterNet, please adjust the batch size in `CenterNet-52.json` to accommodate the number of GPUs that are available to you.

To use the trained model:
```
python test.py CenterNet-52 --testiter 480000 --split <split>
```

We also include a configuration file for multi-scale evaluation, which is `CenterNet-104-multi_scale.json` and `CenterNet-52-multi_scale.json` in this repo, respectively. 

To use the multi-scale configuration file:
```
python test.py CenterNet-52 --testiter <iter> --split <split> --suffix multi_scale
```
or
```
python test.py CenterNet-104 --testiter <iter> --split <split> --suffix multi_scale
```