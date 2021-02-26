## Downloading the TensorFlow Models Repository

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
python3 -m official.vision.beta.train --model_dir=<Directory to model> --mode=train_eval --experiment=retinanet_resnetfpn_coco --config_file="official.vision.beta.configs.experiments.retinanet.resnet50fpn_coco_tfds_tp.yaml"
```

## How to Link a Working YAML

In the repository we provided a generic YAML file to use on any TFDS dataset. Fill it in to work with your specific TensorFlow Dataset.

*Scaling to multiple GPUs here*

## How to Download Your Datasets

### COCO

To get started, you'll need both TensorFlow and TensorFlow-Datasets installed. 

```bash
pip install tensorflow
pip install tensorflow-datasets
```

Be sure to have Python version 3.5 - 3.8

TensorFlow-Datasets allows you to download and store datasets using the provided load() function. To download COCO, we will first need to activate the Python Console.

```bash
python3
```

Once you're there, run the following two commands.

```python
import tensorflow_datasets as tfds

tfds.load('COCO')
```

This will download and store the COCO dataset in **~/tensorflow_datasets/coco**

Note that: COCO is about 40.1 GB large

### ImageNet

[Click here for a tutorial on how to download and properly extract ImageNet.](https://cloud.google.com/tpu/docs/imagenet-setup)

## How to Run Commands With Custom YAML File

Now that we have our YAML file set up, we can start the training process.

In terminal, first change your working directory to **~/models**, and then use the following command:

```bash
python3 -m official.vision.beta.train --model_dir="<Directory to model>" --mode=train_eval --experiment=retinanet_resnetfpn_coco --config_file=<Path to custom YAML>
```

When completed, it will store your finished model in **\<Directory to model\>**.

To evaluate your model use the following command:

```bash
python3 -m official.vision.beta.train --model_dir="<Directory to model>" --mode=eval --experiment=retinanet_resnetfpn_coco --config_file=<Path to custom YAML>
```

