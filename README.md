# RetinaFace_Pytorch
Reimplement RetinaFace with Pytorch

## Installation
##### Clone and install requirements
    $ git clone https://github.com/supernotman/RetinaFace_Pytorch.git
    $ cd RetinaFace_Pytorch/
    $ sudo pip install -r requirements.txt

Pytorch version 1.1.0+ and torchvision 0.3.0+ are needed.

##### Data
1. Download widerface dataset

2. Download annotations (face bounding boxes & five facial landmarks) from [baidu cloud](https://pan.baidu.com/s/1Laby0EctfuJGgGMgRRgykA) or [dropbox](https://www.dropbox.com/s/7j70r3eeepe4r2g/retinaface_gt_v1.1.zip?dl=0)

3. Organise the dataset directory as follows:

```Shell
  widerface/
    train/
      images/
      label.txt
    val/
      images/
      label.txt
    test/
      images/
      label.txt
```

## Train
```
$ train.py [-h] [data_path DATA_PATH] [--batch BATCH]
                [--epochs EPOCHS]
                [--shuffle SHUFFLE] [img_size IMG_SIZE]
                [--verbose VERBOSE] [--save_step SAVE_STEP]
                [--eval_step EVAL_STEP]
                [--save_path SAVE_PATH]
                [--depth DEPTH]
```

#### Example
For multi-gpus training, run:
```
$ CUDA_VISIBLE_DEVICES=0,1,2,3,4,5 python train.py --data_path /widerface --batch 32 --save_path ./out
```

#### Training log
```
---- [Epoch 39/200, Batch 400/403] ----
+----------------+-----------------------+
| loss name      | value                 |
+----------------+-----------------------+
| total_loss     | 0.09969855844974518   |
| classification | 0.09288528561592102   |
| bbox           | 0.0034053439740091562 |
| landmarks      | 0.003407923271879554  |
+----------------+-----------------------+
-------- RetinaFace Pytorch --------
Evaluating epoch 39
Recall: 0.7432201780921814
Precision: 0.906913273261629
```

## Detect
```
$ python detect.py --model_path out/model_epoch_200.pt --image_path 4.jpg
```
<p align="center"><img src="assets/1.jpg" width="640"\></p>
<p align="center"><img src="assets/3.jpg" width="640"\></p>

## Todo: 
- [ ] Wider Face mAP calculation
- [ ] Deformable Convolution
- [ ] More models support
- [ ] Random crop and color distortion
- [ ] Graph Convolution
- [ ] Bug fix
