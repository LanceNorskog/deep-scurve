This Colab notebook runs experiments in training an autoencoder (written in Keras/Tensorflow) to regenerate MNIST digits. 

## Model

The Keras code uses the 'scurve' library to create a mapping for a 32x32 grid. 
MNIST digits are 28x28, so they are extended to 32x32.
The autoencoder takes the set of digits and:
1) feeds it one pixel at a time to an LSTM, 
2) feeds the output of the LSTM to another LSTM,
3) feeds the output of that LSTM to a Dense network using TimeDistributed,
4) which emits one pixel at a time as the output image.

## Training charts

The training is done with three image sets: training, validation, and test. Training checks against the validation set after each epoch. The model is chosen from the lowest level of validation loss (not accuracy!). Training stops if, after 15 epochs, validation loss does not continue to decrease. (The nadir of validation loss is generally accepted as the crossover point between under- and over-training.) After training finishes, we evaluate the model on the second hold-out 'test' data. We save and graph the loss, accuracy, validation loss, validation accuracy, test loss and test accuracy here.

![detailed training](images/lstm_mse_final_2_flyback_extra.png)

How to read this: *loss*, *accuracy*, *val_loss*, *val_accuracy* should be familiar. *test_accuracy* is the accuracy made on the best version of the model against the second holdout 'test' dataset. The horizontal and vertical dashed lines are the final measure of the model: the vertical line as at the lowest value of validation loss, and the horizontal line is the accuracy of the test data. Look at the distance between the red val_accuracy line and the dashed test_accuracy line- this is the measure of how bad the model is. 'delta' is the vertical distance between these two lines at the nadir of the validation loss. 

In a good model, this delta should be very small- the validation accuracy and test accuracy should be very very close. In this chart, the delta is huge because this model is terrible! The job of the LSTMs is to retain a running summary of the pixels recently fed into it, in order to auto encode each pixel. An LSTM with only one hidden neuron of internal state cannot retain much information about the recent pixels.

## Experiments

There are 12 different experiments, 6 LSTM sizes v.s. with&without Hilbert rearrangement. 
They demonstrate conclusively that, at least in a limited design, Hilbert rearrangement causes a major improvement.

The following charts are stripped down to just val_loss, val_accuracy and test_accuracy. 


[colab](https://colab.research.google.com/github/LanceNorskog/deep-scurve/blob/master/notebooks/Scurve_MNIST_Demo.ipynb)


