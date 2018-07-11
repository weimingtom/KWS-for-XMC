# Keyword Spotting for XMC

This repository consists of source code and examples demonstratnig how to realize keyword recognition on the XMC microcontrollers, based on [this project](https://github.com/ARM-software/ML-KWS-for-MCU).

Our implementation depends on the core libraries I2S and DSP. The I2S library receives audio input from the microphone, and the DSP library processes the input signal.

# Background on Speech Recognition

The speech signal is converted to speech features, which are then used as the input of speech recognition algorithms. There exist many established methods of speech feature extraction, and MFCCs (mel frequency cepstral coefficients) belong to the most commonly used features. 

## Feature Extraction
A typical feature extraction process is consited of following steps:

* Preemphasis:
    a high-pass filter can be applied to emphasize the higher frequencies.
* Segmentation and windowing: 
    Hamming window is commonly used.
* Magnitude spectrum from FFT 
* Mel frequency warping:
    the frequency bins are converted to mel frequency bins (on a logarithmic scale)    
* Critical band integration:
    overlapping rectangular filters are applied to each critical band. The sum of the magnitudes in each filter bank is computed and taken logirithm of. 
* Cepstral decorrelation:
    apply discrete cosine transform of the filter bank outputs to get cepstral coeffcients

## Recognition
Neural networks are the current state-of-art in language recognition. 

At the time of writing, this repository uses a 3-layer fully connected neural network. In the network used, each layer has 48 neurons. This small network is trained to recognize four words: left, right, on and off. After quantization, the accuracy of training, validation and test is 93.00%, 89.75% and 88.73% respectively.

# Limitations

# TODO