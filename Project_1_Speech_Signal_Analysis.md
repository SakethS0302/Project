# 1. Speech Signal Analysis

---
* **Description:** Analysis of audio speech signals in time and frequency domains to extract spectral features and pitch characteristics.
* **What We Did:**
  * *Sampled the signal:* Loaded a .wav file and sampled it after reading it as a sequence of amplitude values over time.
  * *Applied FFT(Fast Fourier Transform):* Converted the Time-Domain Waveform into Frequency Domain.
  * *Built a spectrogram:* This shows how frequency changes over time.
* **Outputs:**
  * *Time-Domain Waveform Plot:* This Plot displays amplitude vs time graph useful for spotting silent spots or where the noise is loud.
  <img width="460" height="277" alt="image" src="https://github.com/user-attachments/assets/d681bc3f-5897-4b4c-9664-392a01aca93a" />

  * *Frequency Spectrum Plot:* Shows the entire spectrum of the audio where the peaks indicate dominant frequencies.
  <img width="460" height="277" alt="image" src="https://github.com/user-attachments/assets/3925df28-04b5-4ffd-80a1-acef2ba2843b" />

  * *Spectogram:* A 2D plot with time on one axis, frequency on the other, and color/intensity showing energy at each point.
  <img width="460" height="276" alt="image" src="https://github.com/user-attachments/assets/dfa0e1c8-63ff-4612-a20c-441762ba1f44" />

  * *ZCR/Short-Time Energy Plot:* Shows how Noisy(ZCR) and loud(Energy) the signal is in every time window.
  <img width="460" height="276" alt="image" src="https://github.com/user-attachments/assets/53e60094-4e1d-4cc9-bd6a-a2c3210842d1" />

* **Applications(Real World):**
  * *Time-Domain Waveform Plot:*
    * Seismology - Monitoring earthquake activity through seismograms to measure wave arrival times and peak amplitudes.
  * *Frequency Spectrum Plot:*
    * Telecommunications - Monitoring radio frequency spectrum usage to manage bandwidth allocation and detect signal interference.
  * *Spectrogram:*
    * Sonar & Radar Processing - Detecting underwater targets, marine life, or Doppler frequency shifts over time.
  * *ZCR(Zero-Crossing Rate):*
    * Voice Activity Detection(VAD) - Detecting the presence of human speech vs. background silence or ambient noise in telephony and smart speakers.
  * *Short-Time Energy:*
    * Acoustic Event & Impact Detection - Identifying sudden physical events, such as gunshots, glass breaking, or mechanical thumps in automated security surveillance.

* **Disadvantages:**
  * *Sensitivity to Background Noise:* Standard time-domain and frequency-domain analysis struggles in real-world environments with ambient noise.
  * *Stationarity Assumption:* Traditional Fast Fourier Transforms (FFT) assume the signal is stationary, which fails for dynamic speech signals with rapid transitions.

* **How to fix them:**
  * *Apply Noise Reduction Pipelines:* Pre-process audio with Wiener Filtering, Bandpass Filtering to clean background noise before analysis.
  * *Implement Voice Activity Detection(VAD):* Filter out silence and ambient noise blocks before calculating parameters like Short-Time Energy or Zero-Crossing Rate.

---
