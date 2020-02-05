This Colab notebook runs experiments in training an autoencoder (written in Keras/Tensorflow) to regenerate MNIST digits. 
There are 12 different experiments, 6 LSTM sizes v.s. with&without Hilbert rearrangement. 
They demonstrate conclusively that, at least in a limited design, Hilbert rearrangement causes a major improvement.

The Keras code uses the 'scurve' library to create a mapping for a 32x32 grid. 
MNIST digits are 28x28, so they are extended to 32x32.
The autoencoder takes the set of digits and:
1) feeds it one pixel at a time to an LSTM, 
2) feeds the output of the LSTM to another LSTM,
3) feeds the output of that LSTM to a Dense network using TimeDistributed,
4) which emits one pixel at a time as the output image.
