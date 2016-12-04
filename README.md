# inception-retrain
Standalone version of Tensorflow Inception Retrain. Google Codelabs can be found [here](https://codelabs.developers.google.com/codelabs/tensorflow-for-poets).

This example downloads a pre-trained version of the inception model and re-trains the last layers to recognize custom categories of images. 

In particular we will use photos of flowers

## Steps

### 1. (optional) Download flower files
In a terminal, run the following commands:
```
mkdir tf_files
cd tf_files
curl -O http://download.tensorflow.org/example_images/flower_photos.tgz
tar xzf flower_photos.tgz
rm flower_photos.tgz
cd ..
```

Go check out the files you just downloaded in the `tf_files` folder.

### 2. Retrain Inception

Run the following command (edit paths and training steps as you please)
```
python ./retrain.py \
--bottleneck_dir=./tf_files/bottlenecks \
--how_many_training_steps 500 \
--model_dir=./tf_files/inception \
--output_graph=./tf_files/retrained_graph.pb \
--output_labels=./tf_files/retrained_labels.txt \
--image_dir ./tf_files/flower_photos
```

### 3. Inspect the files created by the training

The `tf_files` folder now contains a lot of new files:

```
tf_files
|- bottlenecks
|- flower_photos
|- inception
    |- classify_image_graph_def.pb
    |- cropped_panda.jpg
    |- imagenet_2012_challenge_label_map_proto.pbtxt
    |- imagenet_synset_to_human_label_map.txt
    |- inception-2015-12-05.tgz
    |- LICENSE
```

read more about their content [here](https://codelabs.developers.google.com/codelabs/tensorflow-for-poets).

### 4. Use the retrained Inception

Let's test the re-training on a daisy image:
```
python ./label_image.py ./tf_files/flower_photos/daisy/21652746_cc379e0eea_m.jpg
```

you should get something like:
```
daisy (score = 0.99071)
sunflowers (score = 0.00595)
dandelion (score = 0.00252)
roses (score = 0.00049)
tulips (score = 0.00032)
```
