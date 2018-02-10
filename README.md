# Tensorflow Ninjago character classification
This is a project to familiarize with [Tensorflow](https://www.tensorflow.org/) using image classification. My kids all love [Ninjago](https://en.wikipedia.org/wiki/Lego_Ninjago), the animated Lego ninja cartoon series, hence the inspiration here!

![Ninjago characters](https://www.sky.com/assets2/lego-ninjago-masters-of-spinjitzu-tile-bd99b78c.jpg)

The basis for this project can be found in [Tensorflow's Image Recognition docs](https://www.tensorflow.org/tutorials/image_recognition). In this project I've retrained the Tensorflow Inception model to add new image classifications. TensorFlow is an open-source software library for dataflow programming across a range of tasks. It is a symbolic math library, and also used for machine learning applications such as neural networks. As always, thank you [Wikipedia](https://en.wikipedia.org/wiki/TensorFlow).

This setup is for a Mac. It will work on Windows (or Linux) as well, but you may need to make some adjustments. 

Let's get Tensorflow fired up. We'll run this in a Virtualenv to keep it separate and interference-free from other Python stuff on our machine. We're running Python 2.7.x here. Please note this will also run with Python 3.x with some minor adjustments to our commands.

## Setup for Mac
Install Tensorflow with Virtualenv. You'll need [pip](https://pip.pypa.io/en/stable/installing/):
```
pip install --upgrade virtualenv
```

Create a Virtualenv environment:
```
virtualenv --system-site-packages ~/tensorflow
```

Activate the Virtualenv environment:
```
cd ~/tensorflow
source ./bin/activate
```

This will change your bash prompt to the following:
```
(tensorflow)$ 
```

Make sure pip ≥8.1 is installed in your Virtualenv:
```
easy_install -U pip
```

Install TensorFlow and all the packages that TensorFlow requires into the active Virtualenv environment:
```
pip install --upgrade tensorflow
```

## Setup for Windows
First [Run the Anaconda Installer](https://repo.continuum.io/archive/Anaconda3-5.0.1-Windows-x86_64.exe).

During installation, check the box to add Anaconda to your PATH.

Once this incredibly long installation is complete, open a fresh command prompt window and create a new conda environment for running tensorflow:
```
conda create -n tensorflow pip python=3.5
```
Activate the tensorflow environment:

```
activate tensorflow
```

Your command prompt should now show:
```
(tensorflow) PATH>
```

Where PATH is the desired directory (i.e. C:\Users\Stuart Ashby).

Now, inside your tensorflow environment, install TensorFlow:
```
pip install --ignore-installed --upgrade tensorflow
```
## Test Tensorflow install
Let’s do a Hello World program in python that uses the TensorFlow package to make sure it’s installed correctly.

Now let’s run a tensorflow “Hello world” program. Instead of creating a new python file, we’ll feed the code into Python one line at a time.

Start python by running the python command:
```
python
```
Now enter each line of python code (don’t include the >>>):
```
>>> import tensorflow as tf
>>> hello = tf.constant('Hello, TensorFlow!')
>>> sess = tf.Session()
>>> print(sess.run(hello))

```

You should see: “Hello, TensorFlow!” 

Congratulations! Your computer is now running one of the most powerful machine learning tools on the planet, created by the original Google Brain Team. Your car will one day be able to drive itself thanks to computers running TensorFlow. You have taken your first step towards becoming a data scientist!

To exit your tensorflow environment type ```deactivate``` to resume run ```activate environment-name``` i.e. ```activate tensorflow```.

## Play with Tensorflow

Clone the repo and CD to the ```image_classification``` dir to run our code:
```
(tensorflow)$ git clone https://github.com/StuartAshby/tensorflow-ninjago-character-classification
(tensorflow)$ cd tensorflow-ninjago-character-classification/image_classification
```

Now we are ready to test out some pre-trained models before we train and test our own Ninjago character classification models. Among the pre-trained models Tensorflow Image Recognition comes with out of the box are ```pomegranates``` and ```pandas```:

Let's see if it will classify a couple pomegranates it's never seen before, based on its training:
```
(tensorflow)$ python classifier.py --image_file images/fruit.jpg
(tensorflow)$ python classifier.py --image_file images/fruit2.jpeg
```

And let's also test some never-before-seen pandas:
```
(tensorflow)$ python classifier.py --image_file images/animal.jpeg
(tensorflow)$ python classifier.py --image_file images/animal2.jpg
```

Excellent! It clearly knows how to classify pomegranates and pandas at >90% confidence. You'll see the result show something along the lines of ```(score = 0.98216)``` or thereabouts.

Next let's see how it does with our Ninjago characters. Unlike my kids, it knows absolutely nothing about Ninjago. 

We'll train it using 20 images of Lloyd and 20 images of Kai; two of the show's characters my kids like best. 20 images is not a lot at all, in fact it's just about the bare minimum. It may be more accurate if we trained it using more pics and adjusted some of the other configurations and/or code. We're going with simple and effective for the purposes of this project.

In our ```images/ninjago``` folder we'll add a ```kai``` dir and a ```lloyd``` dir. I simply grabbed the first 20 good images of each character from Google Images to populate the training image sets. View the images in the path to see what the model was trained on.

Let's let it run 500 training steps -- default is 4,000 so we're shortening it for a shorter run -- Tensorflow will perform much better on GPUs. Handles bottlenecks better. Just sayin'.:
```
(tensorflow)$ python retrain.py --model_dir ./inception --image_dir images/ninjago --output_graph ./output.pb --output_labels ./labels.txt --how_many_training_steps 500
```

Now that we've trained it, let's test our our newly trained model's ability to classify Ninjago characters it has never seen before as either Lloyd or Kai. I grabbed an image of each character from Google Images that was not part of the training set; our model has never laid eyes on these images. I placed the images in ```images/test```.

This is the Lloyd image we're testing:
![Lloyd](https://85toys.com/1593-thickbox_default/lego-ninjago-lloyd-original-minifigure-njo226-from-set-70596.jpg)

And this is Kai:
![Kai](https://c.76.my/Malaysia/lego-ninjago-kai-sleeveless-minifigure-legoland-1504-06-Legoland@9.jpg)

Let's see if it will accurately classify these images:
```
(tensorflow)$ python retrain_model_classifier.py images/test/whoisthis1.jpeg
(tensorflow)$ python retrain_model_classifier.py images/test/whoisthis2.jpeg
```

Hooray! 

With limited training images (only 20) and limited steps (only 500), our model is already able to (fairly) accurately classify Ninjago characters as either Lloyd or Kai. You should have scores in the neighborhood of 70% to 90%. For some reason it does seem to be a little better at classifying Lloyd moreso than Kai.

We can certainly make this more sophisticated, add more characters and pics and steps etc. etc. -- but this is just a fun starter project to showcase the power of Tensorflow's image classification. It has helped me learn more about working with Tensorflow and its capabilities.

To deactivate the Tensorflow Virtualenv and return to your default bash prompt:
```
(tensorflow)$ deactivate
```

Enjoy! Go Ninjago!!!
