#**Traffic-Sign-Classifier-Project**

In this project, you will use what you've learned about deep neural networks and convolutional neural networks to classify traffic signs. Specifically, you'll train a model to classify traffic signs from the German Traffic Sign Dataset.

---

###1. SETUP
Some issues getting Tensorflow-GPU working.
CUDA CuDNN vs. 5.1 dll required in CUDA folder
Restart of KERNEL necessary several times before CUDA was functioning.

###2. Data import and visualization
Class sizes are very uneven from 60 to 750.
Attempt to augment dataset using tf.image.random_flip_up_down(image, seed=None) or tflearn.data_augmentation.DataAugmentation (self) unsuccesful

Training Set:   34799 samples
Validation Set: 4410 samples
Test Set:       12630 samples
Image Shape: (32, 32, 3)
Number of classes = 43
Largest class:  750
Smalles classt:  60

###3. Data preparation
Grayscaling and normalization were helpful in bringing the accuracy from .87 to >.9

###4. Network
The standard LeNet from the course was used with the necessary changes for 32*32 and the output to 43 classes.
Dropout was tested, but did not yield better performance (no overfitting yet?)
An improved LeNet was attempted but did not improve results. 

###5. Training
Reducing the batch size down to 32 and increasing the EPOCHS to 200 was key to getting >.93 accuracy.
Setting the rate to rate = 0.0004 was also helpful to finetune the weights to the required >.93 accuracy
EPOCHS = 200
BATCH_SIZE = 32
rate = 0.0004

###6. Accuracy on test set
Final accuracy on the test data set showed an accuracy of .933
Test Set Accuracy = 0.933

###7. Accuracy on additional images sourced from Google Images.

