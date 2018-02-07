# Tensorflow Ninjago character classification
This is a project to familiarize with Tensorflow using image classification. My kids all love Ninjago, the animated Lego ninja cartoon series, hence the inspiration here!

![Ninjago characters](https://www.sky.com/assets2/lego-ninjago-masters-of-spinjitzu-tile-bd99b78c.jpg)

The basis for this project can be found in [Tensorflow's Image Recognition docs](https://www.tensorflow.org/tutorials/image_recognition).

This setup is for a Mac. Let's get Tensorflow fired up. We'll run this in a Virtualenv to keep it separate and interference-free from other Python stuff on our machine. We're running Python 2.7.x here. Please note this will also run with Python 3.x with some minor adjustments to our commands.

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

Clone the repo and CD to the root project dir:
```
git clone https://github.com/StuartAshby/tensorflow-ninjago-character-classification
cd tensorflow-ninjago-character-classification
```

Now we are ready to test out some pre-trained models before we train and test our own Ninjago character classification models. Among the pre-trained models are ```pomegranates``` and ```pandas```:

Let's see if it will classify a couple pomegranates it's never seen before, based on its training:
```
python classifier.py --image_file images/fruit.jpg
python classifier.py --image_file images/fruit2.jpeg
```

And let's also test some pandas:
```
python classifier.py --image_file images/animal.jpeg
python classifier.py --image_file images/animal2.jpg
```

Excellent! It clearly knows how to classify pomegranates and pandas at >90% confidence. You'll see the result show something along the lines of ```(score = 0.98216)```.

Next let's see how it does with our Ninjago characters. Unlike my kids, it knows absolutely nothing about Ninjago. We'll train it using 20 images of Lloyd and 20 images of Kai; two of the show's characters my kids like best. 20 images is not a lot at all, in fact it's just about the bare minimum. it would be more accurate if we trained it using more pics. 

In our ```images/ninjago``` folder we'll add a ```kai``` dir and a ```lloyd``` dir. I simply grabbed the first 20 good images of each charcater from Google Images to populate the training image sets. View the images in this path to see what the model was trained on.

Let's let it run 500 training steps -- default is 4,000 so we're shortening it for a shorter run -- Tensorflow will perform better on GPUs FWIW:
```
python retrain.py --model_dir ./inception --image_dir images/ninjago --output_graph ./output.pb --output_labels ./labels.txt --how_many_training_steps 500
```

Now that we've trained it, let's test our our newly trained model's ability to classify Ninjago characters it has never seen before as either Lloyd or Kai. I grabbed an image of each character from Google Images that was not part of the training set; our model has never laid eyes on these images. I placed the images in ```images/test```.

This is the Lloyd image we're testing:
![Lloyd](https://85toys.com/1593-thickbox_default/lego-ninjago-lloyd-original-minifigure-njo226-from-set-70596.jpg)

And this is Kai:
![Kai](https://c.76.my/Malaysia/lego-ninjago-kai-sleeveless-minifigure-legoland-1504-06-Legoland@9.jpg)

Let's see if it will accurately classify these images:
```
python retrain_model_classifier.py images/test/whoisthis1.jpeg
python retrain_model_classifier.py images/test/whoisthis2.jpeg
```

Hooray! 

With limited training images (20) and limited steps, our model is able to accurately classify Ninjago characters as either Lloyd or Kai. You should have scores in the neighborhood of 70% to 90%. 

We can certainly make this more sophisticated, add more charcaters and pics and steps etc. etc. -- but this project showcases the power of Tensorflow's image classification and has helped me learn more about the platform.
