## Installation

This tutorial requires:

- Python 3.6 - 3.8.7
- TensorFlow 2.4

and the requirements highlighted in [requirements.txt](https://github.com/tensorflow/models/blob/master/official/requirements.txt).

## Downloading the TensorFlow Models Repository

In terminal, execute the following two commands. 

```bash
cd ~
git clone https://github.com/tensorflow/models.git
```

We will also download the TensorFlow Models' requirements using:

```bash
pip install -r ~/models/official/requirements.txt
```

**Ensure your TensorFlow, Numpy, and PyCocoTools versions are compatible.**

## Training and Evaluation CLI

In terminal first change your working directory to **~/models**, and then run either of the following two commands:

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

To evaluate your model use the following two commands:

For **one GPU**:

```bash
python3 -m official.vision.beta.train --num-gpus 1 --model_dir=<Directory to model> --mode=eval --experiment=retinanet_resnetfpn_coco --config_file="retinanet_tfds_one_gpu.yaml"
```

For **eight GPUs**:

```bash
python3 -m official.vision.beta.train --num-gpus 8 --model_dir=<Directory to model> --mode=eval --experiment=retinanet_resnetfpn_coco --config_file="retinanet_tfds_eight_gpu.yaml"
```

NOTE: If you'd like to use an existing YAML file edit the *--config_file* file parameter to the path of your existing YAML file.

NOTE: When running on a distributed system (Large scale TPU or a GPU cluster) TensorFlow-Datasets restricts the amount of shards to at most eight nodes. This means that you can only have eight distributed replicas at the same time.

## Additional Guides

[Editing a YAML file](https://github.com/esuleman/TFTutorials/blob/master/Editing_YAML.md)

[Downloading Datasets](https://github.com/esuleman/TFTutorials/blob/master/downloading_datasets.md)
