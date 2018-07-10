# mfcc_extractor
A Max based mfcc extractor to be used with Wekinator.

Forked from: https://github.com/cososc/mfcc_extractor

## Description:
Simple MFCC extractor that can be used to differentiate between different vocal tones, e.g. singing vs. screaming.

## Requirements:
* Max 7 from Cycling 74
* Zsa.descriptors from http://www.e--j.com/index.php/download-zsa/
* Wekinator and Wekinator Input Helper from http://wekinator.org/
* Any VST audio plugin, such as a reverb. Valhalla DSP's Freq Echo is fun to play with: https://valhalladsp.com/shop/delay/valhalla-freq-echo/

## Instructions
To run, open the patch in Max 7:
1) Activate the ezdac DSP by clicking the speaker icon
2) Set the sound source to Microphone or Sound File
3) If you chose Sound File, open load a sound file. Use the two boxes next to the Open button to start/stop and loop playback.
4) If the sound does not play, adjust the Input Gain slider
5) Select the number of Mel Band(s) to 16 if it is not already
6) Open Wekinator Input Helper, and set it to listen for 16 inputs on port . (Configure inputs your taste. I tried several different methods to get consistent expression from the MFCC feature extractor, and this seems best for classifying vocal tones like "Singing" and "Screaming.")
7) Open Wekinator and create a new model using 16 inputs and 1 classifier output with 2 classes. (I found SVM to work best for classifying the MFCC data.)
8) Playing sound from either the Microphone or Sound File inputs will calculate 16 bands of MFCCs and send those to the Input Helper. The Input Helper will smooth the MFCCs, then pass them on to Wekinator. Once you've trained the model with Wekinator, it should ouput class values of 1 or 2. The Max patch will recieve that value and use it to turn an effect off or on. (Note that this patch subtracts 1 from the Wekinator Classifier output to map the classifier's classes to the 0 to 1 range of most VST audio effect plugin parameters.)
