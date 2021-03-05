## TensorFlow Vision API with TensorFlow-Datasets(TFDS)

This document provides a brief intro of the usage of builtin command-line tools to run experiements 
in the TensorFlow Vision API with TFDS.

## Installation

This tutorial requires:

- Python 3.6 - 3.8.7
- TensorFlow 2.4 - 2.5 nightly

### Option 1: Installing TensorFlow Models nightly from PyPI (recommended)

In terminal, execuate the following command. It will automatically install all of the requirements needed
for your version of Python and will install TensorFlow nightly.

```bash
pip install tf-models-nightly
```

### Option 2: Downloading the TensorFlow Models Repository manually

In terminal, execute the following two commands.

```bash
git clone https://github.com/tensorflow/models.git
```

We will also download the TensorFlow Models' requirements using:

```bash
cd models
pip install -r official/requirements.txt
```

**Ensure your TensorFlow, Numpy, and PyCocoTools versions are compatible.**

## Training and Evaluation CLI

In terminal first change your working directory to **models**, and then run either of the following two commands:

For **one GPU**:

```bash
wget https://raw.githubusercontent.com/esuleman/TFTutorials/master/retinanet_tfds_one_gpu.yaml

python3 -m official.vision.beta.train --num-gpus 1 --model_dir=<Directory to model> --mode=train_eval --experiment=retinanet_resnetfpn_coco --config_file="retinanet_tfds_one_gpu.yaml"
```

For **eight GPUs**:

```bash
wget https://raw.githubusercontent.com/esuleman/TFTutorials/master/retinanet_tfds_eight_gpu.yaml

python3 -m official.vision.beta.train --num-gpus 8 --model_dir=<Directory to model> --mode=train_eval --experiment=retinanet_resnetfpn_coco --config_file="retinanet_tfds_eight_gpu.yaml"
```

When completed, it will store your finished model in **\<Directory to model\>**

To evaluate your model use either of the following two commands:

For **one GPU**:

```bash
python3 -m official.vision.beta.train --num-gpus 1 --model_dir=<Directory to model> --mode=eval --experiment=retinanet_resnetfpn_coco --config_file="retinanet_tfds_one_gpu.yaml"
```

For **eight GPUs**:

```bash
python3 -m official.vision.beta.train --num-gpus 8 --model_dir=<Directory to model> --mode=eval --experiment=retinanet_resnetfpn_coco --config_file="retinanet_tfds_eight_gpu.yaml"
```

NOTE: To use an existing configuration, edit the **--config_file** parameter to the path of your YAML file.

NOTE: At the time of writing, TensorFlow-Datasets restricts the number of shards to at most eight nodes. This means that you can only have eight distributed replicas at the same time.

## Additional Guides

[Editing the Config File](https://github.com/esuleman/TFTutorials/blob/master/Editing_YAML.md)

[Downloading Datasets in TFDS](https://github.com/esuleman/TFTutorials/blob/master/downloading_datasets.md)
