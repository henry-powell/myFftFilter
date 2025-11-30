# myFftFilter — MATLAB FFT-Based Sub-Frame Filter

myFftFilter is a MATLAB function that applies frequency-selective gain to an audio signal in the spectral domain.  
The function slices the signal into overlapping frames, runs an FFT on each frame, adjusts magnitudes inside two user-defined frequency bands, then reconstructs the processed signal using inverse FFT, Hann windowing, and overlap-add.
Ideal for podcast/dialogue cleanup, audio mastering prep, machine-learning dataset preprocessing, and real-time adaptive audio systems.


---

## Features
- **Frame-based spectral processing** — operates on overlapping sub-frames instead of the whole file at once  
- **Two independent frequency bands** — each defined in Hz with low and high cutoffs  
- **Per-band magnitude scaling** — boost or cut inside each band using linear gain factors  
- **Accurate FFT bin selection** — converts frequency ranges (Hz) to FFT bin indices  
- **Hann windowing** — applied before and after spectral processing to reduce artifacts  
- **Overlap-add reconstruction** — rebuilds a continuous mono signal from processed frames  

---

## Function Signature

```matlab
y = myFftFilter(x, Fs, N, hop, freqRange1, freqRange2, magScalars);
```
	•	x — input mono signal
	•	Fs — sampling rate (Hz)
	•	N — frame length in samples
	•	hop — hop size in samples
	•	freqRange1 — [fLow1, fHigh1] in Hz for band 1
	•	freqRange2 — [fLow2, fHigh2] in Hz for band 2
	•	magScalars — [mag1, mag2] linear gain factors for each band

---

## Usage Example

```[x, Fs] = audioread("yourAudio.wav");

N          = 4096;          % frame length
hop        = 2048;          % hop size
freqRange1 = [100, 250];    % band 1: low / low-mid
freqRange2 = [500, 4000];   % band 2: mid / high
magScalars = [1.5, 0.8];    % boost band 1, cut band 2

y = myFftFilter(x, Fs, N, hop, freqRange1, freqRange2, magScalars);

sound(y, Fs);
```

In this example, magnitudes in 100–250 Hz are boosted to 150% of their original values,
while magnitudes in 500–4000 Hz are reduced to 80%.

---

## File Contents
| File           | Description |
|---------------|------------------------------------|
| MyFftFilter.m | Main MATLAB FFT filtering function |

---

### How to Use
	1.	Place MyFftFilter.m on your MATLAB path or in your working directory.
	2.	Load or record a mono audio signal into MATLAB (e.g., using audioread).
	3.	Choose frame size N, hop size hop, two frequency ranges in Hz, and their gain factors.
	4.	Call myFftFilter with the signal and parameters.
	5.	Listen back with sound(y, Fs) or write to disk with audiowrite.

  ---

  ### Technical Notes
	•	Operates on overlapping frames of length N with hop size hop.
	•	Uses FFT / inverse FFT on each frame to modify magnitudes in two bands only.
	•	Frequency ranges are mapped from Hz to FFT bin indices based on the sampling rate Fs.
	•	Hann windows are applied before analysis and during reconstruction to reduce boundary artifacts.
	•	Final signal is obtained via standard overlap-add of the processed frames.

  ---

### Development Environment
- MATLAB R2025a Update 1 (64-bit, macOS)
- Audio Toolbox enabled

---

## Engineering Relevance
myFftFilter demonstrates core digital signal processing principles used in real-world audio engineering and plugin development:

- **Spectral domain processing** — the same method used in EQs, multiband compressors, and intelligent audio analyzers  
- **Windowed STFT (Short-Time Fourier Transform)** — foundational to time-frequency analysis in audio research  
- **Overlap-add reconstruction** — identical to the workflow used in DAWs and commercial DSP frameworks to avoid artifacts  
- **Selective magnitude shaping** — maps directly to parametric filtering, spectral modeling synthesis, and multiband effects  
- **Scalable design** — the concept of multiple spectral regions with independent gain factors mirrors modern audio plugins with band-based control

This implementation highlights the practical side of DSP theory: understanding how FFT, windowing, and frame coherence work together to shape audio without introducing clicks, distortion, or phase imbalance. It provides a foundation for building more advanced processors such as adaptive filters, vocoders, harmonic enhancers, and AI-assisted spectral tools. 
This project demonstrates my interest in algorithmic audio, DSP engineering, and real-time signal processing — and serves as a foundation for future work in plugin development and machine-learning-assisted audio tools.


  © Henry Powell — Audio DSP Development
