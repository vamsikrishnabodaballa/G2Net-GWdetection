# G2Net-GWdetection

This repository contains code for the [G2Net Gravitational Wave Detection](https://www.kaggle.com/c/g2net-gravitational-wave-detection) competition held on [Kaggle](https://www.kaggle.com/) platform.

###### Description of the competition
GW signals have led researchers to observe a new population of massive, stellar-origin black holes, to unlock the mysteries of neutron star mergers, and to measure the expansion of the Universe. These signals are unimaginably tiny ripples in the fabric of space-time and even though the global network of GW detectors are some of the most sensitive instruments on the planet, the signals are buried in detector noise. Analysis of GW data and the detection of these signals is a crucial mission for the growing global network of increasingly sensitive GW detectors. These challenges in data analysis and noise characterization could be solved with the help of data science.

As with the multi-disciplined approach to the discovery of GWs, additional expertise will be needed to further GW research. In particular, social and natural sciences have taken an interest in machine learning, deep learning, classification problems, data mining, and visualization to develop new techniques and algorithms to efficiently handle complex and massive data sets. The increase in computing power and the development of innovative techniques for the rapid analysis of data will be vital to the exciting new field of GW Astronomy. Potential outcomes may include increased sensitivity to GW signals, application to control and feedback systems for next-generation detectors, noise removal, data conditioning tools, and signal characterization.

G2Net is a network of Gravitational Wave, Geophysics and Machine Learning. Via an Action from COST (European Cooperation in Science and Technology), a funding agency for research and innovation networks, G2Net aims to create a broad network of scientists. From four different areas of expertise, namely GW physics, Geophysics, Computing Science and Robotics, these scientists have agreed on a common goal of tackling challenges in data analysis and noise characterization for GW detectors.

In this competition, you’ll aim to detect GW signals from the mergers of binary black holes. Specifically, you'll build a model to analyze simulated GW time-series data from a network of Earth-based detectors.

![image](/800px-LIGO_measurement_of_gravitational_waves.svg.png)

> *The series of images above were taken from the 2015 paper announcing the discovery of gravitational waves from a pair of merging black holes.*

## Data description

In this competition you are provided with a training set of time series data containing simulated gravitational wave measurements from a network of 3 gravitational wave interferometers (LIGO Hanford, LIGO Livingston, and Virgo). Each time series contains either detector noise or detector noise plus a simulated gravitational wave signal. The task is to identify when a signal is present in the data (target=1).

The parameters that determine the exact form of a binary black hole waveform are the masses, sky location, distance, black hole spins, binary orientation angle, gravitational wave polarisation, time of arrival, and phase at coalescence (merger). These parameters (15 in total) have been randomised according to astrophysically motivated prior distributions and used to generate the simulated signals present in the data, but are not provided as part of the competition data.

Each data sample (npy file) contains 3 time series (1 for each detector) and each spans 2 sec and is sampled at 2,048 Hz.

The integrated signal-to noise ratio (SNR) is classically the most informative measure of how detectable a signal is and a typical level of detectability is when this integrated SNR exceeds ~8. This shouldn't confused with the instantaneous SNR - the factor by which the signal rises above the noise - and in nearly all cases the (unlike the first gravitational wave detection GW150914) these signals are not visible by eye in the time series.

## Files

- **train/** - the training set files, one npy file per observation; labels are provided in a files shown below
- **test/** - the test set files; you must predict the probability that the observation contains a gravitational wave
- **training_labels.csv** - target values of whether the associated signal contains a gravitational wave
- **sample_submission.csv** - a sample submission file in the correct format

I included 3 different ways to solve this problem and use different models for them:
- A solution based on EfficientNet 
- A solution based on a modified EfficientNet - EfficientNetV2, with less number of parameters leading to faster traing time but improved score cannot be guaranteed
- An Ensemble method


## Wavelet transform

A popular way to classify 1D signals is to transform the 1D signal into one of several types of spectrograms and then convert this spectrogram to an image. The image is then fed to a pretrained CNN which is fine-tuned during training. Transformation to the frequency domain is quite compute intensive, so we would really like to perform this function on the GPU. Tensorflow currently has no continous wavelet transform (CWT), so we have to make our own. Thankfully, this is a quite simple task using Keras custom layer.




References
- [CQT G2Net EfficientNetB1[TPU Training]](https://www.kaggle.com/miklgr500/cqt-g2net-efficientnetb7-tpu-training-w-b?scriptVersionId=67485043)
- [CQT G2Net EfficientNetV2B0[TPU Training]](https://www.kaggle.com/itsuki9180/cqt-g2net-efficientnetv2b0-tpu-training)
- [[1] G2Net - Smart Ensembling](https://www.kaggle.com/somayyehgholami/1-g2net-smart-ensembling)

If you find the above references useful, please don't forget to upvote.
