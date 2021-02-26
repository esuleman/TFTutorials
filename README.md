# Train RetinaNet with COCO

## Downloading TensorFlow Models

Prior to training RetinaNet we will need to download the TensorFlow Models repository.

In terminal, execute the following two commands. 

```bash
cd ~
git clone https://github.com/tensorflow/models.git
```

Once the repository is downloaded, add **~/models** to your *PythonPath*. Add the following to your .bashrc file.

```bash
export PYTHONPATH=$PYTHONPATH:~/models
```

We will also download all of the TensorFlow Models' requirements using:

```bash
pip3 install -r ~/models/official/requirements.txt
```

**Ensure your TensorFlow, Numpy, and Pycocotools versions are compatible.**

## Linking a working YAML

Now that we have TensorFlow models all set up, we can use the training scripts provided to us with the COCO dataset and train a RetinaNet model. In **~/models** create and open a file named *my_retinanet.yaml*. Here we will set up the variables needed for training and evaluation.

Here is an example YAML file for training RetinaNet using a single GPU. 

```yaml
# my_retinanet.yaml
runtime:
  distribution_strategy: 'one_device'
  num_gpus: 1
  mixed_precision_dtype: 'float32'
  train_data:
    tfds_data_dir: <Directory to tensorflow_datasets>
    tfds_name: 'coco'
    tfds_split: 'train'
    drop_remainder: true
    dtype: float32
    global_batch_size: <Change to suit machine>
    is_training: true
  validation_data:
    tfds_data_dir: <Directory to tensorflow_datasets>
    tfds_name: 'coco'
    tfds_split: 'validation'
    drop_remainder: true
    dtype: float32
    global_batch_size: <Change to suit machine>
    is_training: false
```

Here is an example YAML file for training RetinaNet using 8 GPUs. 

```yaml
# my_retinanet.yaml
runtime:
  distribution_strategy: 'mirrored'
  num_gpus: 8
  mixed_precision_dtype: 'float32'
  train_data:
    tfds_data_dir: <Directory to tensorflow_datasets>
    tfds_name: 'coco'
    tfds_split: 'train'
    drop_remainder: true
    dtype: float32
    global_batch_size: <Change to suit machine>
    is_training: true
  validation_data:
    tfds_data_dir: <Directory to tensorflow_datasets>
    tfds_name: 'coco'
    tfds_split: 'validation'
    drop_remainder: true
    dtype: float32
    global_batch_size: <Change to suit machine>
    is_training: false
```

## CLI Commands to Train and Evaluate Model

Now that we have our YAML file set up, we can start the training process.

In terminal, first change your working directory to **~/models**, and then use the following command:

```bash
python3 -m official.vision.beta.train --model_dir=".myRetinaNetModel.model" --mode=train --experiment=retinanet_resnetfpn_coco --config_file="my_retinanet.yaml"
```

When completed, it will store your finished model in **~/models/myRetinaNetModel/model**.

The following command will run an evaluation of the model:

```bash
python3 -m official.vision.beta.train --model_dir=".myRetinaNetModel.model" --mode=eval --experiment=retinanet_resnetfpn_coco --config_file="my_retinanet.yaml"
```

