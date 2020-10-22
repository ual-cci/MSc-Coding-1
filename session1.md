# Session 1: Sound Part One

# Oscillation

- Fundamental basis of all periodic phenomena
- Not just useful for sounds, but also images
- `sin(x)` function creates a sine wave
- This is a wave, or waveform
- `maxiOsc` object

## Air moving

- Wave goes above 0. --> Speaker moves forward
- Wave goes below 0. --> Speaker moves backward

_The position of the speaker is the PHASE of the wave._

## Frequency

Waves don’t just have a phase. They also have _frequency_

- This is how often they move up and down each second - measured in hertz (hz) (also called 'Cycles Per Second (cps)').
- Waves that oscillate more than around 20 times per second take on a quality of continuos sounds, and not separate pulses
- Interestingly, the same is roughly true for images (fps)
- Oscillations below 20hz are called “Low Frequency” (LFOs)

--

## All about time

- Both sound and video are time based
- Interesting fusion occurs around 20Hz
- Getting things to happen at the right time is an important computational problem

--
## Amplitude

Waves also have an amplitude.

- This is how much they move up and down.
- In the real world, this is how much air they are moving.
- In the computer, we have a different situation.

## Adding sounds together

- In the computer, the audio output should vary between -1 and 1
- This is a linear measurement, not in dB - i.e. not logarithmic
- When you add sounds, they combine linearly and can create distortion
- At maximum, `1+1=2` ...which will cause clipping

## Adding sounds together

- When we add sounds together, strange things happen
- The sounds interfere with each other
  - Beating
  - Amplitude modulation - (multiplication)
  - Frequency modulation - (controlling frequency with another oscillator)
  
## Beating
- When two sinewave oscillators of different frequencies are added together, they interact to alter the amplitude
- This is because they cycle across each other. Sometimes, one will be at -1, while the other is at 1
- So the result becomes 0 at these points
- What you hear is the sound fading in and out.
- We call this 'beating'
- The beat frequency (how often it fades in and out) is equal to the difference between the two input frequencies.
  
## Amplitude Modulation

- A common example of amplitude modulation (AM) is when we multiply two sinusoidal oscillators together
- The output is two signals whose frequencies are the sum and the difference of the two input frequencies
- So if you multiply two sine waves together with frequencies of 400hz & 500hz, you will instead hear 900hz and 100hz

## Frequency Modulation
- We can use the output of a sinewave oscillator to control the frequency of another
- We do this by setting the frequency of the carrier oscillator, and adding the output of the second oscillator (the modulator) to it.
- If we don't change the amplitude of the modulator, not much will happen, because it will simply be adding a value between 1 and -1
- When we increase the amplitude of the modulator (i.e. change the 'modulation index'), this doesn't change the amplitude of the carrier - the sound output doesn't get louder.
- If the frequency of the modulator is greater than the threshold of pitch perception (20 hz), increasing the modulation index makes the sound brighter
- i.e. the frequency content of the signal increases in complexity as you increase the modulation index
- The higher the modulation index, the more sidebands are created, increasing the brightness of the sound
- If the carrier and modulator are factors or multiples of each other, there is less beating (the sounds are harmonics of one another. If not, there is increased beating (the sounds are inharmonic) and eventually, noise (they become highly complex).
- You can use this technique to do lots of things, including generating pseudo-random numbers.
- John Chowning demonstrated that you could theoretically use this technique to simulate almost any sound with enough parameterised modulators.
- https://ccrma.stanford.edu/people/john-chowning

# Session #1 Homework

Make sure you're familiar with how the MIMIC platform works.

Make sure you have created an account on the MIMIC platform.

Make a fork of this documemt :

https://mimicproject.com/code/69704316-d8d8-7623-f0c6-316cb983f0b9

Use it as a basis for carrying out the following tasks:

- Using at least 4 oscillators, create a continuous, drone-based sound texture or sound bed.

- Use two of the oscillators to control parameters of the other two oscillators.

- Make the sound texture vary continuously over a period of 1 minute through the use of low-frequency oscillators, so that the sound texture develops over the entire period.

Extra credit:

- By researching documents on the MIMIC platform, try to work out how to use a filter.
