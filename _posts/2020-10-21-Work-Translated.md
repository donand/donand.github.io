---
layout: post
title: My Work at Translated
---

Hello everyone,

I am writing this post to show some results of the work I'm doing at Translated.<br>

I'm working on Text to Speech. I'm doing applied research and the goal is to generate very natural speech in different laguages, with the ability to control the style of the generated speech. The concept of the style of speech is not easy to define, it's the combination of a lot of different aspects like prosody, emphasis, speaking rate, pitch, etc.
For this reason, it's very hard to manually define what the style is, and then the methods that require handcrafted features in order to define the style don't work.


# Results
I am starting with the results, because who wants to read all the boring details about the models!

The best results are in Italian for now, but I'm working hard to achieve the same quality also in other languages :)

Here there are some videos dubbed with the artificial voices:

<iframe src="https://drive.google.com/file/d/1pPNHyZlRPtYs-nWCFUM0LCbqPeKmcVr9/preview" width="640" height="480"></iframe>


# The Models
In 2020 some end-to-end models for TTS stated showing up, but they are still in a developing phase, and they are not as mature as the old cascade setting. So TTS is made of two models, the first that is the synthesizer that generates mel spectrograms from text, and the second one is the vocoder, that generates the final waveform from the spectrograms.
The spectrogram is a compressed and lossy representation of the audio in the frequency domain, and this is needed in order to make the task easier for the synthesizer.
I am also using an additional audio encoder (Style Encoder) that generates a style vector from a reference audio, and this vector is passed to the synthesizer in order to apply the desired style to the generated speech.

I tried a lot of different models with different resulting quality, but in the end I came up with the following selection:
- Tacotron 2 [1] as the Synthesizer
- WaveRNN [2] as the Vocoder
- Global Style Tokens [3] as the Style Encoder
