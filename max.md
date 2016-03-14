# MAX
## MSP
### Sound
- Continuous rising and falling of air pressure creates a wave of sound
- *Amplitude* is the amount of change with respect to the normal atmospheric pressure
- Peak amplitude refers to the greatest change in pressure achieved by the wave
- Sound waves are periodic because each cycle of the wave occurs in an equal interval
- Frequency is the number of cycles of the wave in one second. Period is inversely proportional.
- Any sound that contains more than a single frequency is a *complex tone*.
- As a sound dies down, frequencies die at different rates, this helps us perceive timbre of a sound
- The combination of frequencies and amplitudes present in a sound are called its *sound spectrum*
- Each individual frequency is called a *partial*
- When partials are all integer multiples of the same fundamental frequency, the sound is said to have a *harmonic spectrum*
- Each component of a harmonic spectrum is called a *harmonic (partial)*
- Phase is an offset in time by some fraction of a cycle
- Each time the fundamental frequency is multiplied by a power of 2, the pitch increases by one octave
- If the frequencies are not integer multiples of a single fundamental frequency, the wave does not repeat periodically - *Inharmonic partials*
- When the partials have no apparent mathematical relationship we perceive the sounds as *noise* - a sound with many random frequencies and amplitudes
- All frequencies present in equal proportion is *white noise*
- The change in amplitude of a sound over the course of its duration is the *amplitude envelope*
- Loudness is perceived in terms of ratios of amplitude ie a sound with double the amplitude wont sound double as loud
- We use a logarithmic scale to describe loudness with the unit *decibels (dB)*

> level in dB = 20 log10 (A/A0) - where A0 is the reference sound

- If we consider the max possible ampltude as a reference to be = 1, then a sound with amplitude 0.5 has 1/2 the amplitude

> 20 log 10 (0.5/1) = 20 (-0.3) = -6 dB

- Each halving of amplitude is a difference of *~-6dB*

### Digital sound
- The number of samples of a sound taken per second is the *sampling rate*
- We need to sample at more than double the rate of the frequency to properly represent a sound
- 1/2 the sampling rate is called the *Nyquist rate*
- *Aliasing* (or foldover) occurs when a frequency gets folded into the range below it ie sample rate 16000hz -> highest frequency = 8000hz -> a signal at 9000hz would be misrepresented as 7000hz
- Frequencies above the Nyquist frequency end up as negative frequencies (the amount over ie 1000hz in the above example), which we are unable to perceive as a any different to the Nyquist frequency minus the negative part (8000-1000 = 7000hz).

### Basics
- MSP objects run much faster than MAX objects so they can accurately produce the 41000 samples needed per second, MAX objects run ~1000 times per second
- MSP objects can be thought of as a description of an instrument, the sound you hear is a result of all the calcuations in the patch at the moment in time, a *signal network*
- dac~, adc~, ezadc~, ezdac~ and adstatus are the only objects that can turn on or off the MSP audio network from within a patcher
- use the *start message* with a loadmess object to begin the audio as soon as the patch opens
- By default start stop messages flow to ALL open max patches, use the startwindow message to start processing only in the affected window
- To control the level of a signal (amplitude) multiply each sample by a scaling factor, ie half the volume -> multiply by 0.5
- *Zipper noise* occurs when there are sudden and drastic changes in amplitude which cause discontinuities in a signal
- line~ and \*~ togethor can be used to create an *envelope*
- We can send up to 64 pairs (value, time) of numbers to a line~, the line will interpolate between all the values, taking the amount of time specified to get there
- Any time 2 signals are added to the same inlet, those signals are added togethor and their sum is used
- Patch cords in MSP dictate the order of calculations to be made before the block of sample is passed onto the next stage
- send and receive objects can be used to communicate remotely without patch cords
  - send~ locations can be changed with a set message
- Semi-colons can be used in message objects to transmit values to receive objects by their name
- Two waves with different frequencies will only come into phase at a rate equal to the difference in their frequencies ie 1000Hz + 1002Hz = in phase 2 times per second
- If you need to combine a fixed and a changing value in a MSP signal chain, you need an object that outputs a constant value as a signal
- The sig~ object can be used to convert a number into a singal

### Additive & Modular synthesis

## MSP Objects
- \*~: multiplies the signal in its left inlet by whatever comes into the right (signal, or number)
  * supplying a signal in the right inlet lets us fade in / out a sound
- Atodb: converts amplitude to dB, max amplitude = 1
- buffer~: An object that stores a set of values, either loaded in or programmed that can be read later on
  * pass a name as an argument to identify the buffer
  * messages can be sent to load audio, resize or clear the memory
  * replace or read are messages that can be sent along with the name of file you want to load. The buffer is sized to fit the audio
- cycle~: Wavetable oscillator, it reads through a list of 512 values at a specified rate, looping back to the beginning when it reaches the end, this simulates a repeating periodic waveform. You can supply your own values
  * receives a frequency in its left inlet (Hz)
  * passing a buffer name to the cycle will make it read values from the buffer. The cycle will default to use 512 samples.
  * buffer_offset can be used to set the start point to read from the buffer
  * buffer_sizeinsamps can be used to change the size of the wave table
  * the right inlet takes a phase offset value in the range 0-1
- dac~: expects signals in the range -1.0 to 1.0 and converts them to sound, signals outside the range will cause distortion
- ezdac~: same as dac except it is hard wired to outputs 1 and 2
- gain~: a slider to control the output amplitude of a signal
- gate~: used to route an input signal that second inlet to one (or none) of the outlets
  * takes a number to indicate the number of outputs
- line~: line segment generator, allows us to specify a duration for MAX to interpolate between our starting and our ending signals, number, or amplitude
  * left inlet takes a target value and a time (ms)
  * takes value/time pairs of numbers, value being the target and time how long
  * send a '0,' as the first argument to immediately move to the first value/time pair (same as sending 'value=0 time=0')
- loadbang: sends a bang to its out put when the patch is loadced, can be used to initialize variables when the patch is loaded
- phasor~: a signal generator that outputs a ramp from 0 to 1 at a given frequency (sawtooth signal)
- receive~:
- send~:
- sig~: convert a numerical message (int/float) to a signal
- slider~: send out a value based on the position of the bar, the range of values can be set to constrain the numbers that are output

## Glossary
* Beat (difference) frequency: the rate of the beats that occur between 2 waves of different frequencies coming in and out of phase 1000Hz + 1002Hz = beat frequency 2 Hz
* Portamento: gradual gliding from one signal to another
