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

- If we conside the max possible ampltude as a reference to be = 1, then a sound with amplitude 0.5 has 1/2 the amplitude

> 20 log 10 (0.5/1) = 20 (-0.3) = -6 dB

- Each halving of amplitude is a difference of *~-6dB*

### Digital sound
- The number of samples of a sound taken per second is the *sampling rate*
- We need to sample at more than double the rate of the frequency to properly represent a sound
- 1/2 the sampling rate is called the *Nyquist rate*
- *Aliasing* (or foldover) occurs when a frequency gets folded into the range below it ie sample rate 16000hz -> highest frequency = 8000hz -> a signal at 9000hz would be misrepresented as 7000hz
- Frequencies above the Nyquist frequency end up as negative frequencies (the amount over ie 1000hz in the above example), which we are unable to perceive as a any different to the Nyquist frequency minus the negative part (8000-1000 = 7000hz).
