---
title: Speaker Recognition using Python and Machine Learning (EE412 - Fractals in Engineering)
layout: default
---
# Speaker Recognition using Python and Machine Learning #

## Introduction / Project Overview ##

I had been wanting to learn more about machine learning (as well as Python), and I was really excited to take a "Neural Network and Fuzzy Logic" course my last semester. But unfortunately, it got canceled due to low enrollment. So when I found out that my Fractals class had a final project with a free choice of topic, I took advantage of the opportunity and did mine on machine learning.

For this project, I used the popular machine learning algorithm Gaussian Mixture Models (GMM) to train models to recognize the speakers of some commonly used "command" words. This project was implemented in Python, which I'm still new to, so I followed a base code and modified it to run on Python 3. 

## Index ##

[Summary / tl;dr](#summary--tldr) <br>
[Background / Theory](#background--theory) <br>
[Connection to Fractals](#connection-to-fractals) <br>
[Machine Learning Process](#machine-learning-process) <br>
— [Dataset Selection](#dataset-selection) <br>
— [Pre-processing](#-pre-processing) <br>
— [Feature Extraction](#feature-extraction) <br>
— [Model Training](#model-training) <br>
— [Validation Testing](#validation-testing) <br>
[Results and Discussion](#results-and-discussion) <br>
[Future Work](#future-work) <br>
[Repository](https://github.com/nolanschan/Speaker-Identification-using-GMMs)

## Summary / tl;dr ##

### Process ###
- — Pre-processed voice clips from selected dataset
- — Performed feature extraction with Mel-frequency cepstral coefficients and delta-Mel-frequency cepstral coefficients
- — Trained models using Gaussian Mixture Models (GMM) algorithm
- — Tested validity of models by using unseen voice clips

### Results ###
Due to the small amount of training data that the models were given, in general, the system was able to correctly recognize the speaker about 2/3 of the time. The exception was when the model was trained on a number of instances of the same word, and then asked to recognize the speaker saying the same word. In that case, the system was able to recognize the speaker 100% of the time.

It was also accidentally found that the system seemed able to recognize between different words, implying that the system could be used to perform speech recognition instead/as well.

## Background / Theory ##

### Speaker Recognition ###

Speaker recognition: To identify a person based on the characteristics of their voice

This is different from speech recognition, which identifies the words spoken, regardless of speaker. 

Speaker recognition can be text-dependent (system can only recognize the speaker when using specific command/trained words) or text-independent (system can recognize the speaker using any words). For example, smart home assistants are text-indepdent — after they learn the user's voice from a (relatively) small amount of voice data, they're able to recognize the user, regardless of what they're saying.

Speaker recognition systems can also be extended to perform speaker verification/authentication. By combining with speech recognition such that the system learns the users' names, such a system can determine whether the speaker is who they say they are. 

### Time Domain vs Frequency Domain ###

Most people are used to seeing voice/sound as a time domain waveform, like this one:

<img src="/projects/speakerrec/assets/6_yes_1_wave.png" width="800">

This is the waveform of one of the speakers in the dataset saying the word "yes", plotted using Librosa in Python. Knowing what word was said, you can kinda see in the wave the structure of the word: "ye-s". But as we learned in school/engineering classes, time domain representation doesn't give us a whole lot of useful information to work with. So we use frequency domain instead.

So here's the same voice clip in the frequency domain, or its spectrogram:

<img src="/projects/speakerrec/assets/6_yes_1_spec.png">

Well it tells us what frequencies are there but... it's not a lot to work with.

Here's another spectrogram of another speaker saying the same word:

<img src="/projects/speakerrec/assets/1_yes_1_spec.png">

Well you can tell it's different, but it's not <i>that</i> different.

### How Humans Hear and the Mel Frequency Scale ###

How are we humans able to differentiate between and recognize all the voices we hear? Well one thing to remember is that we don't hear differences in frequencies, or pitches, linearly. For example, 100Hz and 200Hz sound farther apart than 1000Hz and 1100Hz, even though both sets have a 100Hz difference between them.

So this is where the Mel frequency scale comes in. 

The Mel frequency scale is a nonlinear scale which more closely approximates the human auditory system's response to different pitches, or frequencies. There isn't a standardized formula for calculating the Mel frequency equivalent, but here's a popular one:

$$m = 2595\log_{10}(1\ +\ \frac{f}{700})$$

And when plotted against the Hertz scale, it looks like this:

<img src="/projects/speakerrec/assets/melhzplot.png"> <br>
(You can read more about the Mel scale on [Wikipedia](https://en.wikipedia.org/wiki/Mel_scale), which is also where I got the image of the above plot.)

### Mel-scaled Spectrogram ###

From the formula and the plot we can see that humans hear different frequencies logarithmically. So what if we plot our spectrogram using the Mel scale?

<img src="/projects/speakerrec/assets/6_yes_1_melspec.png">

Well that's... better. But it's still pretty sparce. Are we missing something else? Maybe something that we also hear logarithmically?

Oh! Volume! How could we forget about the decibel scale? So let's try plotting our Mel-scaled spectrogram with the amplitude scaled in dB.

<img src="/projects/speakerrec/assets/6_yes_1_melspecdB.png">

Wow look at that! That's a lot more information available for us (or a computer) to analyze.

In fact, another popular method for training speaker recognition models is to feed these Mel-/dB-scaled spectrograms into a neural network. Then it simply becomes an image classification problem. It was actually one of the methods that I looked into for this project, but since I wanted to learn about machine learning before trying to get into deep learning, I decided against using it.

### (Mel frequency) Cepstrum ###

Because we're not using the spectrogram images, we need to use some other way to extract some features to train our models with. One common way in audio signal processing to represent the power spectrum of a sound is by its "cepstrum". Or more specifically, for audio signals, the Mel frequency cepstrum (MFC).

A cepstrum is basically the "spectrum of a spectrum". It shows the rate of change/periodicity in the different spectrum bands. For the Mel frequency cepstrum, the power spectrum is mapped to the Mel scale.

Just as we can derive Fourier coefficients for a Fourier series, we can also derive Mel frequency cepstral coefficients (MFCCs) for a MFC. This is commonly done by:
- — Taking the Fourier Transform of a signal
- — Mapping the power spectrum to Mel scale
- — Taking the log of the Mel-scaled power spectrum
- — Taking the inverse Fourier Transform of the power spectrum to the "quefrency" domain (time in samples)
- — The resulting amplitudes are the cepstral coefficients.

(You can read more about the MFC on [Wikipedia](https://en.wikipedia.org/wiki/Mel-frequency_cepstrum))

Although MFCCs give us information about the spectrum of a speech signal, they're limited to a particular frame. This is similar to the study of motion: A moving  particle can be described by its (instantaneous) position, but to know its motion, we need to find its velocity and acceleration, the first and second derivatives of its position. Likewise, speech signals are time-varying, and there's information in the way the MFCCs change.

In this case, the first and second derivatives are called the differential and acceleration coefficients, or the delta and delta-delta MFCCs.

The delta MFCCs can be found using the following formula:

$$d_t\ =\ \frac{\sum_{n=1}^{N} n(c_{t+n}\ -\ c_{t-n})}{2\sum_{n=1}^{N} n^2}$$

where $$d_t$$ is the delta coefficient, from frame $$t$$ computed in terms of the static coefficients $$(c_{t+n}\ -\ c_{t-n})$$, and a typical value for $$N$$ is 2. The delta-delta coefficients can be calculated similarly by replacing the static coefficients in the formula with the delta coefficients.

Researchers have found that using just the delta coefficients improved the performance of speech (and speaker) recognition systems.

You can read more about them (and about MFCCs as well) [here](https://wiki.aalto.fi/display/ITSP/Deltas+and+Delta-deltas) and [here](http://practicalcryptography.com/miscellaneous/machine-learning/guide-mel-frequency-cepstral-coefficients-mfccs/).

### Gaussian Mixture Models ###

Gaussian Mixture Models (GMM) is a commonly-used method in unsupervised machine learning. A lot of information, as well as the math behind it, can be found on this [blog](https://towardsdatascience.com/gaussian-mixture-models-explained-6986aaf5a95)(, from which I also grabbed some images below). For the purpose of this project, here's a brief conceptual summary.

Let's say we've extracted the features from our dataset, and plotted on a graph, they look like this:

<img src="/projects/speakerrec/assets/gmm1.png">

We can see pretty clearly that they can easily be grouped into 2 clusters like this:

<img src="/projects/speakerrec/assets/gmm2.png">

This is the basis behind another popular alagorithm, "K-means clustering". This method finds the mean, or centroid, of each cluster (μ1 and μ2 in the image) and their distances from each datapoint. The datapoints are grouped into a cluster based on proximity until the results converge. This is known as a <i>hard clustering method</i>, in which each point belongs to only one cluster.

Gaussian Mixture Models (GMMs), on the other hand, is a <i>soft clustering method</i>. Each cluster is represented by a Gaussian, which describes the probability that the data points belong to that cluster.

<img src="/projects/speakerrec/assets/gmm3.png">

Some important differences to note are that data points can belong to more than 1 cluster, such that cluster boundaries can overlap, and the clusters are not necessarily circular, as illustrated by this image from a SciPy GMM [demo](https://scikit-learn.org/stable/auto_examples/mixture/plot_gmm_covariances.html).

<img src="/projects/speakerrec/assets/gmm4.png">

## Connection to Fractals ##



## Machine Learning Process ##

### Dataset Selection ###

For this project, I used the ["Speech Command Dataset"](https://ai.googleblog.com/2017/08/launching-speech-commands-dataset.html) created by the TensorFlow and Google AIY teams. It contains 65,000 1-second-long utterances of 30 short words submitted by members of the public through the AIY website. These include commonly-used "command" words (yes, no, stop, on, off), digits, directions, as well as some miscellaneous words and names.

My motivation behind using this dataset rather than other popular speech datasets like VoxForge was because of the fact that this project was for a Fractals course. I wanted to have example clips of different people saying the same words multiple times in order to show the self-similarities in the time and frequency domains.

As a first-time project, I decided to use a smaller subset of the dataset. 6 speakers were randomly selected based on the criteria that they had 5 clips for each word, and ended up being 5 male and 1 female. The words chosen were "yes", "no", "stop", "go", and "up". During the whole process, between 5-11 clips/speaker were used for training, and 1 clip/speaker was used for testing.

### Pre-processing ###

As the clips were submitted by the public, the quality vary vastly. It also seemed that speakers often recorded clips of the same words consecutively, so there was common background noise in all clips. I wanted to make sure the model was based on the voice and not the background noise as much as possible, so some pre-processing was done before training.

All data were pre-processed manually using Audacity as following:
- — Trim word
- — Align to start
- — Zero-padding for 1-sec clip

### Feature Extraction ###



### Model Training ###



### Validation Testing ###

## Results and Discussion ##

## Future Work ##

## Repository ##

