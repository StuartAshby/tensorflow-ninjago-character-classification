# Tensorflow Ninjago character classification
This is a project to familiarize with Tensorflow using image classification. 

This setup is for a Mac.

Install Tensorflow with Virtualenv. You'll need pip:
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
(tensorflow)$ easy_install -U pip
```

Install TensorFlow and all the packages that TensorFlow requires into the active Virtualenv environment:
```
(tensorflow)$ pip install --upgrade tensorflow
```

Clone the repo and CD to the root dir:
```
git clone https://github.com/StuartAshby/tensorflow-ninjago-character-classification
cd tensorflow-ninjago-character-classification
```

Now we are ready to test out some pre-trained models before we train and test our own Ninjago character classification models. Among the pre-trained models are ```pomegranates``` and ```pandas```:

Let's see if classify a couple pomegranates it has never seen before, based on its training:
```
```

And let's also test some pandas:
```
```

Excellent! It clearly knows how to classify pomegranates and pandas.

Next let's see how it does with our Ninjago characters. Since it knows absolutelyh nothing about Ninjago, we'll train it using 20 images of Lloyd and 20 images of Kai; 2 of the characters my kids like best. 20 images is not a lot at all, in fact it ius just about the bare minimum. it would be more accurate if we trained it using more pics. Let's let it run 500 training steps -- default is 4,000 so we're shortening it for a shorter run -- Tensorflow will perform better on GPUs FWIW:
```
```

Now that we've trained it, let's test our our newly trained model's ability to classify Ninjago characters it has never seen before as either Lloyd or Kai:
```
python retrain_model_classifier.py images/test/whoisthis1.jpeg
python retrain_model_classifier.py images/test/whoisthis2.jpeg
```

With limited training images (20) and limited steps, our model is able to accurately classify Ninjago characters as either Lloyd or Kai. We can make this more sophisticated, but this project showcases the power of Tensorflow's image classification.


