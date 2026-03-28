# Analog-Audio-Synthesizer (555 + RC filtering + Vibrato)
Analog audio synthesizer using 555 timers and cascaded RC filters to transform a square wave into a smoother and more musical waveform.

# Why I built this

I wanted to understand how musical sound is actually generated electrically.

So instead of using pre-built modules or digital synthesis, I built an analog signal chain from scratch:

generate a waveform → shape it → modulate it → listen to it

The goal was to see how waveform shape and modulation directly affect what we hear.

# What I built

An analog synthesizer using:

1) A 555 timer as the main oscillator
2) A second 555 timer as a low-frequency modulator (vibrato)
3) cascaded RC low-pass filters
4) An LM358 amplifier driving a speaker

The main oscillator generates the tone.
The filters reshape it.
The low-frequency oscillator adds slight pitch variation (vibrato), which makes the sound feel more natural.

# Signal flow

Low-frequency oscillator (vibrato)
→ Main oscillator (square wave)
→ RC filter stages
→ Amplifier
→ Speaker

# What’s going on

The main oscillator produces a square wave.

A square wave isn’t a single frequency.
It consists of:

1) A fundamental frequency
2) Multiple higher-frequency sine components

Those higher-frequency components are what make it sound harsh.

Filtering reduces those components, which smooths the waveform and changes how it sounds.

Then the low-frequency oscillator slightly modulates the pitch over time.
That small variation is what gives the sound a more musical, less static feel.

# What actually mattered

This ended up being mostly about tuning, not just building.

I kept adjusting resistor and capacitor values until the sound hit a balance:
not too harsh, not too dull, and not too weak.

Too little filtering → harsh, buzzy
Too much filtering → muffled and low amplitude

Then adding vibrato changed everything.
Without it, the tone felt flat and artificial. With it, even a simple waveform started to feel more alive.

# Failure 1: no amplification

At first, I filtered the signal and sent it straight to the speaker.

It didn’t work properly.
Each filter stage reduced the signal, and the output was too weak to drive the speaker.

Adding the LM358 amplifier fixed this and made the filtered signal usable.

# Failure 2: incorrect filter structure

In the first filter attempt, I connected the capacitor directly to ground without a series resistor.

Result:

almost no meaningful filtering
sound stayed harsh

After adding a 1kΩ resistor before the capacitor, the filter started working as expected:

high-frequency content dropped
waveform smoothed
sound changed clearly
# Why cascading stages mattered

A single RC stage barely changes the sound.

With multiple stages:

harmonics are reduced progressively
waveform smoothing becomes noticeable
the sound moves closer to a sinusoidal tone

Filtering made it smoother.
Vibrato made it feel musical.

# The math behind it



From AC circuit theory:

𝑍
𝐶
=
1
𝑗
𝜔
𝐶
Z
C
	​

=
jωC
1
	​


As frequency increases, the capacitor’s impedance decreases.

So:

high-frequency signals see a low-impedance path to ground and are attenuated
lower-frequency signals pass through with less attenuation

Cutoff frequency:

𝑓
𝑐
=
1
2
𝜋
𝑅
𝐶
f
c
	​

=
2πRC
1
	​


Each RC stage contributes partial attenuation, and cascading them increases the overall effect.

# Circuit schematic

# Signal before vs after filtering



square wave: sharp transitions, high harmonic content
filtered signal: smoother waveform, reduced high-frequency components
# Demo 

(Insert your edited video here)

Includes:

raw vs filtered sound
pitch sweep
filtering effect
vibrato from the low-frequency oscillator
# Notes

Small changes in resistor and capacitor values had a large impact on:

sound harshness
smoothness
signal strength
overall feel of the tone

Most of the work was in tuning the circuit until the waveform sounded right, then adding modulation to make it feel less static.

# Future improvements
active filters for sharper cutoff control
adjustable vibrato depth and rate
envelope shaping (ADSR)
PCB implementation
