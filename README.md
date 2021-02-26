## Downloading the TensorFlow Models Repository

Before starting ensure you have a Python version between 3.5 - 3.8.7. This tutorial is written in a bash terminal.

In terminal, execute the following two commands. 

```bash
cd ~
git clone https://github.com/tensorflow/models.git
```

Once the repository is downloaded, add **~/models** to your *PythonPath*. Add the following to your .bashrc file.

```bash
export PYTHONPATH=$PYTHONPATH:~/models
```

We will also download the TensorFlow Models' requirements using:

```bash
pip3 install -r ~/models/official/requirements.txt
```

**Ensure your TensorFlow, Numpy, and PyCocoTools versions are compatible.**

## How to Run Commands

In terminal, first change your working directory to **~/models**, and then run the following command:

```bash
python3 -m official.vision.beta.train --model_dir=<Directory to model> --mode=train_eval --experiment=retinanet_resnetfpn_coco --config_file="official.vision.beta.configs.experiments.retinanet.resnet50fpn_coco_tfds_tp.yaml"
```

When completed, it will store your finished model in **\<Directory to model\>**

To evaluate your model use the following command:

```bash
python3 -m official.vision.beta.train --model_dir=<Directory to model> --mode=eval --experiment=retinanet_resnetfpn_coco --config_file="official.vision.beta.configs.experiments.retinanet.resnet50fpn_coco_tfds_tp.yaml"
```

**Note: These YAML files are configured for training on a TPU**

## Editing YAML file

In the repository we provided a generic YAML file to use on any TFDS dataset. You can fill in the empty fields with your specifications or remove them if you would like to use the default values.

[Click here for the YAML file](https://github.com/esuleman/TFTutorials/blob/master/example.yaml)

*Scaling to multiple GPUs here*

## How to Download Your Datasets

### coco

To get started, you'll need both TensorFlow and TensorFlow-Datasets installed. 

```bash
pip install tensorflow
pip install tensorflow-datasets
```

TensorFlow-Datasets allows you to download and store datasets using the provided load() function. To download COCO, we will first need to activate the Python Console. Once you're there, run the following two commands.

```python
import tensorflow_datasets as tfds

tfds.load('coco/2017')
```

This will download and store the coco dataset in **~/tensorflow_datasets/coco**

Note that: coco is 25.20 GB large. 

### ImageNet

Visit this website: http://www.image-net.org/challenges/LSVRC/2012/downloads

You will need to register for an account and get a valid ID. Once you get an ID, run the following commands:

```bash
export PATH_TO_TFDS=<Path to tensorflow_datasets directory>
export DOWNLOADS_DOWNLOAD_DIR=$PATH_TO_TFDS/downloads
export MANUAL_DOWNLOAD_DIR=$PATH_TO_TFDS/downloads/manual

wget http://image-net.org/challenges/LSVRC/2012/dd31405981ef5f776aa17412e1f0c112/ILSVRC2012_img_train.tar
wget http://image-net.org/challenges/LSVRC/2012/dd31405981ef5f776aa17412e1f0c112/ILSVRC2012_img_test.tar
wget http://image-net.org/challenges/LSVRC/2012/dd31405981ef5f776aa17412e1f0c112/ILSVRC2012_img_val.tar

python3 -m tensorflow_datasets.scripts.download_and_prepare --datasets=imagenet2012 --data_dir=$PATH_TO_TFDS --download_dir=$DOWNLOADS_DOWNLOAD_DIR --manual_dir=$MANUAL_DOWNLOAD_DIR
```

This will result in an ImageNet datasets in the .tfrecord format that is compatible with TensorFlow-Datasets.

To test if ImageNet is properly loaded, simply enter the Python Console and enter the following commands:

```python
import tensorflow_datasets as tfds

tfds.load('imagenet2012')
```

Note that: ImageNet is 155.84 GB large. It is suggested to have 300GB of storage. 

## How to Run Commands With Custom YAML File

Now that we have our YAML file set up, we can start the training process.

In terminal, first change your working directory to **~/models**, and then use the following command:

```bash
python3 -m official.vision.beta.train --model_dir="<Directory to model>" --mode=train_eval --experiment=retinanet_resnetfpn_coco --config_file=<Path to custom YAML>
```

When completed, it will store your finished model in **\<Directory to model\>**

To evaluate your model use the following command:

```bash
python3 -m official.vision.beta.train --model_dir="<Directory to model>" --mode=eval --experiment=retinanet_resnetfpn_coco --config_file=<Path to custom YAML>
```

