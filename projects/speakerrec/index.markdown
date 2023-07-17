---
title: Speaker Recognition using Python and Machine Learning (EE412 - Fractals in Engineering)
layout: default
---
# Speaker Recognition using Python and Machine Learning #

## Introduction ##
<p></p>

I had been wanting to learn more about machine learning (as well as Python), and I was really excited to take a "Neural Network and Fuzzy Logic" course my last semester. But unfortunately, it got canceled due to low enrollment. So when I found out that my Fractals class had a final project with a free choice of topic, I took advantage of the opportunity and did mine on machine learning.

For this project, I used the popular machine learning algorithm Gaussian Mixture Models (GMM) to train models to recognize the speakers of some commonly used "command" words. This project was implemented in Python, which I'm still new to, so I followed a base code and modified it to run on Python 3. 

[Full project details](/projects/speakerrec/detail)

## Project Overview ##

-  <u>Type</u>: Individual
-  <u>Timeframe</u>: Approx. 1 month
-  <u>Relevant Concepts/Skills</u>: Research, machine learning, Gaussian Mixture Model, (audio) signal processing
-  <u>Tools</u>: Audacity, Python, Jupyter Notebook, NumPy, SciPy, Python Speech Features, scikit-learn, Librosa
-  <u>Deliverable(s)</u>: Final presentation
<p></p>

## Procedures ##

<ul style="list-style-type:disc;line-height:100%">
  <li>Researched machine learning and algorithmns</li>
  <li>Pre-processed voice clips from selected dataset</li>
  <li>Performed feature extraction with Mel-frequency cepstral coefficients and delta-Mel-frequency cepstral coefficients</li>
  <li> Trained models using Gaussian Mixture Models (GMM) algorithm</li>
  <li>Tested validity of models by using unseen voice clips</li></ul>
<p></p>

## Results ##

Trained models achieved 67-100% accuracy in speaker recognition depending on test data used.

![](/projects/speakerrec/assets/results1.png)

![](/projects/speakerrec/assets/results2.png)

Due to the small dataset used (about 5-13 seconds, including silence, of voice clips per speaker), in general the model is only successful about 4-5 out of 6 times at identifying the speaker. The model tends to be more successful if the test word is one that it has "heard" at least once. 

However, when the model is trained on the same word (4x) used for testing, even though the test clip is previously unseen, the model is able to identify the speaker 100% of the time.

It was also accidentally found that the system seemed able to recognize between different words, implying that the system could be used to perform speech recognition instead/as well.

## Future Work ##
<p></p>

To improve performance, more voice samples (available in the main Speech Commands Dataset) will likely be needed for training. Data can also be augmented (for example by introducing noise) in order to increases the robustness of the model.

Other ML/DL algorithms could be implemented instead/in addition to GMM.

It should also be possible to extend this model to perform speech recognition and/or speaker verification.

## Repository ##
<p></p>

The full code can be found in the repository [here](https://github.com/nolanschan/Speaker-Identification-using-GMMs).
