# WakeWordDetection - Update in Progress!
## Overview of this project
This repository is a documentation of Wakeword detection model development with Pytorch intended for use with QT robots. 
- [X] Selection of wakeword to be trained: "Hello QT"
- [X] Data Collection: collected approximately 50-60 real world audio from 10 different collaborators
- [X] Data Preprocessing/ Augmentation: Cleaning and formatted the data and augmented to upsample to 600 examples.
- [x] Model Design Selection: Researched for best and efficient architecture for real world application purpose (referenced Michael Phi)
- [x] Training / Testing: Best Test Accuracy: **0.9448529411764706**
- [ ] Deployment to as the real world application
- [ ] Maintenance    

### Data Collection

We began by recording the wakeword, "Hello QT", in order to prevent possible bias with just one person recording audio for hundreds of times, I asked 10 people to voluntarily record themselves speaking the wakeword. 

### Data Preprocessing / Augmentation

In order to make the data as uniformed as possible, I have preprocessed all the audio into 3 second chunk with sample rate of 16000 Khz. Sample rate was specified based on the sample rate of microphone installed with QT robots. 

We collected 50 original audio with 10 unique individuals' voices, however, this is significantly lower than the number of correct label samples, so we used augmentation technique to upsample the 50 original audio to 600 unique augmented audio data.

We used audiomentation, a python audio augmentation library, to augment the data by adding random background environmental noises, reverbation, and pitch shifting to the samples.  

We also randomly select the environmental background noises as the 0 label examples. In addition to that, we have used commonvoice dataset as the 0 label examples, which was augmented with background noises. 

   **Little Note 1: The order of augmentation matters!**  If you add background noise before you apply pitch shifting, the pitch shift also affects the pitch of the background noise. So be aware of the order in which you apply the augmentation!
   
   **Little Note 2: Sample rate of the audio files** Think about the sample rate of the audio file we are dealing with, if the audio sample rate of the background noise is greater than the audio file which we intend to augment, downsampling must be performed, which hurts the execution time. 
   
 ### Model Design Selection
 First, we want to mention two different type of neural networks, RNN and CNN.
 CNN, convolutional neural network which is used for imagery data. Convolution simplifies the complex and grained representation of images. RNN, recurrent neural network on the other hand, is used for temporal problems such as language processing, speech recognition and etc.
 
 We selected LSTM, long short term memory network which is a special kind of RNN as the model architecture. 
 
 ### Training / Testing

We use the LSTM model with 32 hidden units and 1 layer. 
We selected AdamW as the optimzer and BCEWithLogitLoss, Binary cross entropy with logit loss. We use BCEWithLogitLoss because it is more stable than using sigmoid and BCELoss separately.

We ran 100 epoch on the dataset and achieved the best test accuracy of **0.9448529411764706**

## Reference 

1. The A.I. Hacker - Michael Phi, https://youtu.be/ob0p7G2QoHA
2. Michael Phi, github, https://github.com/LearnedVector/A-Hackers-AI-Voice-Assistant
3. 
