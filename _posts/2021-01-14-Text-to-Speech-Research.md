---
layout: post
title: My Research on Text to Speech
---

Hello everyone,

I am writing this post to show some results of the work I'm doing at [Translated](https://translated.com/). Translated is a translation company based in Rome, Italy.<br>

Here I'm working on Text to Speech. I'm doing applied research and the goal is to generate very natural speech in different laguages, with the ability to control the style of the generated speech.<br>
The concept of style of speech is not easy to define, it's the combination of a lot of different aspects like prosody, emphasis, speaking rate, pitch, etc.<br>
For this reason, it's very hard to manually define what the style is, so the methods that use handcrafted features in order to define the style don't work.


# Results
Let's start with the results, because who wants to read all the boring details about the models!

The best results are in Italian for now, but I'm working hard to achieve the same quality also in other languages :)

Here there are some videos dubbed with artificial voices.<br>
If you cannot play the videos and the audio, please visit this page with Google Chrome.

<iframe style="text-align: center; width: 100%; margin-top: 20px" src="https://drive.google.com/file/d/1ZfV51EMJFmJkP1brQeVpDZapqou6iRCz/preview" width="480" height="360"></iframe>

<iframe style="text-align: center; width: 100%; margin-top: 20px" src="https://drive.google.com/file/d/1hwbfuc23T4OxlHZSu0LQBbb21AZX34Ar/preview" width="480" height="360"></iframe>

But these voices can also speak with different styles: they can talk normally, they can whisper, they can even shout! Or maybe they can tell a story like a book or a documentary!

<iframe style="text-align: center; width: 100%;" src="https://drive.google.com/file/d/1yX1pBunJRZ3xTDGlRmAtZuJDqzFSys1m/preview" height="80"></iframe>


# The Models
In 2020 some end-to-end models for TTS started showing up, but they are still in a developing phase, and they are not as mature as the old cascade setting.<br>
For this reason, I use a TTS system made of two models, the first is the synthesizer, that generates mel spectrograms from text, and the second one is the vocoder, that generates the final waveform from the spectrograms.<br>
The spectrogram is a compressed and lossy representation of the audio in the frequency domain. The use of a more compact representation of the audio instead of the raw waveform, is useful in order to make the task easier for the synthesizer, because it generates an output with roughly 500 or 1000 timesteps instead of the 200k timesteps of a waveform.<br>
But of course this comes at the cost of using a lossy representation of the audio, and the effort to get back the information and reconstruct the final waveform is left to the Vocoder.

For the style, I am using an additional audio encoder, the Style Encoder, that generates a style vector from a reference audio, and this vector is passed to the synthesizer in order to apply the desired style to the generated speech.<br>
The reference audio is used to define the style that we want to generate at inference time, and it's usually a sample chosen from the dataset.

I tried a lot of different models with different final quality, training complexity, speed, and in the end I came up with the following selection:
- Tacotron 2 *[1]* as the Synthesizer
- WaveRNN *[2]* as the Vocoder
- Global Style Tokens *[3]* as the Style Encoder


<br>

------


[1] [Natural TTS Synthesis by Conditioning WaveNet on Mel Spectrogram Predictions](https://arxiv.org/pdf/1712.05884.pdf)<br>
[2] [Efficient Neural Audio Synthesis](https://arxiv.org/pdf/1802.08435.pdf)<br>
[3] [Style Tokens: Unsupervised Style Modeling, Control and Transfer in End-to-End Speech Synthesis](https://arxiv.org/pdf/1803.09017.pdf)