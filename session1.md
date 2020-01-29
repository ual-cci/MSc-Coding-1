# Session 1: Sound Part One

# Oscillation

- Fundamental basis of all periodic phenomena
- Not just useful for sounds, but also images
- `$sin(x)$` function creates a sine wave
- This is a wave, or waveform
- `maxiOsc` object

## Air moving

- Wave goes above 0. --> Speaker moves forward
- Wave goes below 0. --> Speaker moves backward

_The position of the speaker is the PHASE of the wave._

## Frequency

Waves don’t just have a phase. They also have _frequency_

- how often they move up and down each second
- waves that oscillate more than around 20 times per second take on a quality of continuos sounds, and not separate pulses
- Interestingly, the same is roughly true for images (fps)
- Oscillations below 20hz are called “Low Frequency” (LFOs)

--

## All about time

- Both sound and video are time based
- Interesting fusion occurs around 20 Hz
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
- `$1+1=2$` ...not so great for your speakers. But sounds nice.


## Adding sounds together

- When we add sounds together, strange things happen
- The sounds interfere with each other
  - Beating
  - Amplitude modulation

# Session #1 Practical

Work through the first few examples.

Using at least 4 oscillators, create a continuous, drone-based sound texture or sound bed using procedural C++ audio.

Use two of the oscillators to control parameters of the other two oscillators. Try to use a filter.

Make the sound texture vary continuously over a period of 1 minute through the use of low-frequency oscillators, so that the sound texture develops over the entire period.