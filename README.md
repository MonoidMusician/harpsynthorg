Experimenting with a harpsichord-like synthesizer in Max/MSP, performing Royer's Le Vertigo.

[YouTube](https://youtu.be/05AL-Oq3e2Y)

[Soundcloud](https://soundcloud.com/violonscheelist/le-vertigo)

This project was in large part inspired by the fabulous recording of [Jean Rondeau](https://youtu.be/DzxlMfUzqIM), which I highly recommend watching since the sound quality, performance, and videography put my attempts to shame.

<img src="https://raw.githubusercontent.com/MonoidMusician/harpsynthorg/main/Le%20Vertigo.png" alt="Orange Le Vertigo logo with white text over a dark orange textured circle" width="300">

## Instrument

The harpsichord is an obvious choice for electronic music experiments, at least to me:
it is a percussion instrument, so only the timing of strikes and releases needs to be calculated.
There isn't any real velocity control, either! All strokes will sound at the same intensity.

Obviously the name “harpsynthorg” is a pun on harpsichord and synthesizer: I decided I liked the velar “g” at the end rather than the “d” to make up for replacing the velar “ch” with the dental “th”.

## Synthesizer

The synthesizer was thrown together really quickly with a basic idea of combining sine waves and square waves with different decay rates, so the sound starts out more metallic but then mellows out.
This survived pretty intact from the initial idea to present day, with some expanded scope: added overtones, more sophisticated decay.

Although I was obviously driven in search of sounds I am familiar with, I didn't do any formal research, this was all my a priori knowledge.

Some of the technical details are that the overtones are slightly out of tune (fundamental, 2.005, 3.004, 2.005^2, and 5.000 times the fundamental), decaying at exponents of 1, 1, 2, 4.5, and 4.5 respectively.
The amplitude of the fundamental strengthens with increasing pitch (from 0.45 to 1.0) while the first overtone attenuates (from 0.5 to 0.2).
This was in an attempt to get a brighter sound in the bass registers but it did not go far enough and leads to a muddy, quiet sound.
The remaining overtones are fixed at 0.27, 0.05, and 0.04 amplitude respectively.

The square wave decays with the 4.5 exponent of the higher overtones.
It additionally has a random amount of twang, beginning below pitch, rising above pitch, and falling back at pitch within 180ms.

All of the waves are approximately corrected for perceived loudness using [A-weighting](https://en.wikipedia.org/wiki/A-weighting#A).

There's some issues with clicks at the beginnings of notes, but it's much improved from my early drafts (now mostly affecting super low notes).
The main issue is that the volume sounds quiet even though it's running near max amplitude, and I suspect this is a timbre issue as I said above, or there could be other reasons I just do not know about.

## Performance

I wanted to create a performance of Le Vertigo, a flashy and engaging piece for harpsichord by Pancrace Royer, from the French Baroque period.
(They really went all out on the theatrics in the French Baroque period, I tell ya.)

My main concern was adding a system of rubato so it wouldn't sound robotic.
I eventually settled on a system where I can enter linear ramps to tweak timing within the measure (subdivided into three beats).
That is, leaving it at zero plays the measure completely in time (relative to a specified tempo), while adjustments upwards delay the notes in time and adjustments downwards play them sooner.
So the adjustment at the start of the measure determines whether it comes in delayed (high) or early (low), and the adjustment at the end determines the length of the measure: full upwards means the measure is a whole beat longer.
It is thus common to have a sudden jump at the end of the timing function, just to delay the next measure slightly! Or “give it space/place the downbeat” as we musicians like to waffle.

I architected my own custom system of timing within Max/MSP to fit this idea in, while also giving myself slightly higher-level building blocks to fashion the piece out of.
(I literally wrote the piece as a program within Max.)
In doing so, I was able to ensure that we only ever need to translate from musical time to realtime, and never the other way around, which simplified many things about the implementation.
(It also means that invalid musical times, like beat 10 of measure 2, still match up to a real time, like beat 1 of measure 5, instead of disappearing.)

All of the timing is driven through the event system in Max/MSP, so it isn't necessarily sample-accurate, but it seems decently accurate/reproducible to my ear.
And a little variation is okay, that's the point!

I didn't have the chance yet to implement ornaments like trills or rolled chords, but I think they would be fun to add in.
Obviously this means it is missing a lot of the French Baroque pinache, but the music still survives well I think!
There's some rests missing, but otherwise the implementation is very accurate to the score, barring any mistakes I may have made in transcription.


