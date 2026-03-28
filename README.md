# Analog-Audio-Synthesizer (555 + RC filtering + Vibrato)
Analog audio synthesizer using 555 timers and cascaded RC filters to transform a square wave into a smoother and more musical waveform.

# Why I built this

I wanted to understand how musical sound is actually generated electrically.

So instead of using pre-built modules or digital synthesis, I built an analog signal chain from scratch:

generate a waveform → shape it → modulate it → listen to it

The goal was to see how waveform shape and modulation directly affect what we hear.

# What I built

An analog synthesizer using:

* A 555 timer as the main oscillator
* A second 555 timer as a low-frequency modulator (vibrato)
* cascaded RC low-pass filters
* An LM358 amplifier driving a speaker

The main oscillator generates the tone.
The filters reshape it.
The low-frequency oscillator adds slight pitch variation (vibrato), which makes the sound feel more natural.

# Signal flow


# What’s really going on

The main oscillator produces a square wave.

A square wave isn’t a single frequency.
It consists of:

* A fundamental frequency
* Multiple higher-frequency sine components

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

Then adding vibrato elevated it a bit more.
Without it, the tone felt flat and artificial.

# Failure 1: no amplification

At first, I filtered the signal and sent it straight to the speaker.

It didn’t work properly.
Each filter stage reduced the signal, and the output was too weak to drive the speaker.

Adding the LM358 audio amplifier fixed this and made the filtered signal usable.

# Failure 2: incorrect filter structure

In the first filter attempt, I connected the capacitor directly to ground without a series resistor.

Result:

* almost no meaningful filtering
* sound stayed harsh

After adding a 1kΩ resistor before the capacitor, the filter started working as expected:

* high-frequency content dropped
* waveform smoothed
* sound changed clearly
  
# Why cascading stages mattered

A single RC stage barely changes the sound.

With multiple stages:

harmonics are reduced progressively
waveform smoothing becomes noticeable
the sound moves closer to a sinusoidal tone

Filtering made it smoother.
Vibrato made it feel musical.

# The math behind it
## Capacitor impedance
$$
Z_C = \frac{1}{j\omega C}, \quad \omega = 2\pi f
$$

As frequency increases, the capacitor’s impedance decreases.

That means high-frequency components see a very low-impedance path to ground and get shunted away, while lower-frequency components see a higher impedance and continue through the circuit.

In practice, this is exactly what creates the low-pass filtering effect

## RC low-pass behavior
$$
H(j\omega) = \frac{1}{1 + j\omega RC}
$$
$$
|H(j\omega)| = \frac{1}{\sqrt{1 + (\omega RC)^2}}
$$

As 
𝜔
ω increases, the magnitude drops, meaning higher-frequency components are attenuated more strongly.

## Why the square wave sounds harsh
$$
x(t) = \frac{4}{\pi} \left( \sin(\omega t) + \frac{1}{3}\sin(3\omega t) + \frac{1}{5}\sin(5\omega t) + \cdots \right)
$$

A square wave is made up of a fundamental frequency plus multiple higher-frequency harmonics.

Those higher harmonics are what give it that sharp, buzzy sound.
Once the filter attenuates them, the waveform is left mostly with the fundemental which sounds smoother.



# Circuit schematic

# Signal before vs after filtering


# Demo 

(Insert your edited video here)

Includes:

raw vs filtered sound
pitch sweep
filtering effect
vibrato from the low-frequency oscillator
# Notes

Small changes in resistor and capacitor values had a large impact on:

* sound harshness
* smoothness
* signal strength
* overall feel of the tone

Most of the work was in tuning the circuit until the waveform sounded right, then adding modulation to make it feel less static.

# Future improvements
* active filters for sharper cutoff control
* adjustable vibrato depth and rate
* envelope shaping (ADSR)
* PCB implementation
