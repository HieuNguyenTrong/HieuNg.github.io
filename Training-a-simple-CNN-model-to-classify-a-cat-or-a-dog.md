
"""
@Descr: Train a simple model for classifying a cat or a dog
@Created Date: 
@Modified Date: 2018 Dec 03
@author: Hieu.NguyenTrong
"""
# Building the CNN
# importing the Keras libraries and packages
from keras.models import Sequential
from keras.layers import Convolution2D
from keras.layers import MaxPooling2D
from keras.layers import Flatten
from keras.layers import Dense
from keras.layers import Dropout
from matplotlib import pyplot
from keras.constraints import maxnorm

# initialising the CNN
classifier = Sequential()

# -- Step 1 - First Convolution 
classifier.add(Convolution2D(filters= 64, kernel_size= 3, 
                             input_shape=(64, 64, 3), kernel_constraint=maxnorm(3),
                             data_format="channels_last",                       
                             activation="relu"))
# Max Fooling
classifier.add(MaxPooling2D(pool_size=(2,2)))
# Dropout
classifier.add(Dropout(0.5))

# Second Convolution
classifier.add(Convolution2D(filters= 128, kernel_size= 3, kernel_constraint=maxnorm(3),
                             activation="relu"))
classifier.add(MaxPooling2D(pool_size=(2,2)))
classifier.add(Dropout(0.5))


# -- Step 3 - Flattening
classifier.add(Flatten())
 
# -- Step 4 - Fully Connected 
classifier.add(Dense(128, activation="relu",  kernel_constraint=maxnorm(3)))
classifier.add(Dropout(0.5))
classifier.add(Dense(1, activation="sigmoid"))
classifier.summary()
 # Compiling the CNN
classifier.compile(optimizer = "adam", loss ="binary_crossentropy", metrics = ['accuracy'])
 
 # Fitting the CNN 
from keras.preprocessing.image import ImageDataGenerator
 
# Image augumentation
train_datagen = ImageDataGenerator(
        rescale=1./255,
        shear_range=0.2,
        zoom_range=0.2,
        horizontal_flip=True)

test_datagen = ImageDataGenerator(rescale=1./255)

training_set = train_datagen.flow_from_directory('C:/dataset/training_set',
                                target_size=(64, 64),
                                batch_size=32,
                                class_mode='binary')

test_set = test_datagen.flow_from_directory(
        'C:/dataset/test_set',
        target_size=(64, 64),
        batch_size=32,
        class_mode='binary')

# Fitting model
history = classifier.fit_generator(training_set,
                        steps_per_epoch=8000,
                        epochs=15,
                        max_queue_size=10,
                        workers=10,
                        validation_data=test_set,
                        validation_steps=2000)

# Visualising results
pyplot.plot(history.history["acc"], label = "train")
pyplot.plot(history.history["val_acc"], label = "test")
pyplot.legend()
pyplot.show()

pyplot.plot(history.history["loss"], label = "train")
pyplot.plot(history.history["val_loss"], label = "test")
pyplot.legend()
pyplot.show()

# Saving models
classifier.save("C:/models/cnn_epoch_15.h5")

# Predicing 
from keras.models import load_model
from keras.preprocessing import image
import numpy as np
import matplotlib.pyplot as plt

model = load_model('C:/models/cnn_epoch_15.h5')
img_path = 'C:/dataset/single_prediction/cat_or_dog_1.jpg'
imag = image.load_img(img_path, target_size=(64, 64))
plt.imshow(imag)

imag = image.img_to_array(imag)
imag = np.expand_dims(imag, axis=0)

model.predict(imag)

