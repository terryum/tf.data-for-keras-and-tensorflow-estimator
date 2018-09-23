# tf.data examples for keras and estimator models


**Please refer to [the jupyter notebook file](https://github.com/terryum/tf.data-for-keras-and-tensorflow-estimator/blob/master/0-TFData-For-Keras-Estimator.ipynb) for details.**

<br>

## Motivation
The official [Tensorflow guide](https://www.tensorflow.org/guide/keras#input_tfdata_datasets) says that tf.data.Dataset can be directly fed into model.fit in Keras since TF 1.09. However, it is an absolute lie at the moment of TF 1.10, Sept 2018, as you can see from the following images. 

![Tensorflow site](https://github.com/terryum/tf.data-for-keras-and-tensorflow-estimator/blob/master/img1_TFsite.jpg)
![Error](https://github.com/terryum/tf.data-for-keras-and-tensorflow-estimator/blob/master/img2_error.jpg)

I have spent three days to figure out what the problem is, but it turns out that **IT IS JUST NOT WORKING**. Instead, it is working with **TF-Nightly** (TF 1.12-dev at this moment) rather than TF 1.10, as discussed [here](https://github.com/tensorflow/tensorflow/issues/21894) and [here](https://medium.com/tensorflow/training-and-serving-ml-models-with-tf-keras-fd975cc0fa27). 

For those who may suffer from the similar problems that I had, I made [this tutorial code](([https://github.com/terryum/tf.data-for-keras-and-tensorflow-estimator/blob/master/0-TFData-For-Keras-Estimator.ipynb])) to show how you can incorporate tf.data into your Keras model. 

<br>

## Contents

**[IMPORTANT] You should first install `tf-nightly` or `tf-nightly-gpu` via `pip install tf-nightly` or `pip install tf-nightly-gpu` if you have intalled a tensorflow under 1.11 version  

* This code consists of four parts as followings: 

#### 0. Data & Model preparation
Load MNIST dataset and build a simple 2-layer MLP model (784-40-40-10) using Keras.

#### 1. Train the model usgin a tf.data.Dataset loaded from numpy data on the memory.
Assumption: The amount of your data is enough small, thus you can load them on the memory.
Solution: Make a tf.data.Dataset and train the model using it.

#### 2. Train the model usgin a tf.data.Dataset loaded from a TF record file.
Assumption: The amount of your data is to large to load on the memory.
Solution: Create a TFRecord file first, and make a tf.data.Dataset from it.

* Estimator is a standard ML model for real-world products which is ready to deploy on google cloud.

#### 3. Use a pre-made estimator and tf.data made from a TF record file.
This code first shows how tf.data can be naturally incorporated into a pre-made estimator provided by Tensorflow APIs.

#### 4. Use a custom estimator created by using Keras
You may want to build a custom model using Keras and train it using your large-scale data. One of the easiest ways to do it is (i) to write a TF record file, (ii) make a tf.data.Dataset from it, (iii) buile a model using Keras, (iv) convert the model to an estimator using `model_to_estimator`, (v) train the model like the previous example.

<br>

## Thanks
I hope this tutorial could save your time. Feel free to use or change this code for your own purpose. If you are intereted in deep learning research, you can follow me on [twitter](https://twitter.com/TerryUm_ML) and have interesting discussions. 
