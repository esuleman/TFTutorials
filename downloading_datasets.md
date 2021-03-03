## How to Download Datasets in TensorFlow-Datasets

This document provides a brief tutorial on downloading COCO and Imagenet2012 in TensorFlow-Datasets

### COCO

To get started, you'll need both TensorFlow and TensorFlow-Datasets installed. 

```bash
pip install tensorflow
pip install tensorflow-datasets
```

TensorFlow-Datasets allows you to download and store datasets using the provided **load()** function. To download COCO, we will first need to activate the Python Console. Once you're there, run the following two commands.

```python
import tensorflow_datasets as tfds

tfds.load('coco/2017', split = 'train')
```

This will download and store the COCO dataset in **~/tensorflow_datasets/coco**

NOTE: [COCO](https://www.tensorflow.org/datasets/catalog/coco) is 25.20 GB large. 

### ImageNet

Visit the [Official ImageNet Website]( http://www.image-net.org/challenges/LSVRC/2012/downloads)

You will need to register for an account and get a valid ID. Once you get an ID, run the following commands:

```bash
export PATH_TO_TFDS=<Path to tensorflow_datasets directory>
export DOWNLOADS_DOWNLOAD_DIR=$PATH_TO_TFDS/downloads
export MANUAL_DOWNLOAD_DIR=$PATH_TO_TFDS/downloads/manual
export ID=<Your ID here>

wget -c http://image-net.org/challenges/LSVRC/2012/$ID/ILSVRC2012_img_train.tar -O $MANUAL_DOWNLOAD_DIR/ILSVRC2012_img_train.tar
wget -c http://image-net.org/challenges/LSVRC/2012/$ID/ILSVRC2012_img_test.tar -O $MANUAL_DOWNLOAD_DIR/ILSVRC2012_img_test.tar
wget -c http://image-net.org/challenges/LSVRC/2012/$ID/ILSVRC2012_img_val.tar -O $MANUAL_DOWNLOAD_DIR/ILSVRC2012_img_val.tar

python3 -m tensorflow_datasets.scripts.download_and_prepare --datasets=imagenet2012 --data_dir=$PATH_TO_TFDS --download_dir=$DOWNLOADS_DOWNLOAD_DIR --manual_dir=$MANUAL_DOWNLOAD_DIR
```

This will result in an ImageNet dataset in the .tfrecord format that is compatible with TensorFlow-Datasets.

To test if ImageNet is properly loaded, simply enter the Python Console and enter the following commands:

```python
import tensorflow_datasets as tfds

tfds.load('imagenet2012', split = 'train')
```

NOTE: [ImageNet](https://www.tensorflow.org/datasets/catalog/imagenet2012) is 155.84 GB large. It is suggested to have 300GB of free storage prior to installation.
