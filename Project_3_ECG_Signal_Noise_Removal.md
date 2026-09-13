# 3. ECG Signal Noise Removal

---
* **Description:** Biomedical signal processing pipeline to filter high-frequency noise and powerline interference from Electrocardiogram(ECG) data.
* **What We Did:**
  * We build a test ECG signal with a realistic ECG Waveform(a P-QRS-T heartbeat shape made from overlapping Gaussian pulses) and then injected three noises(Baseline Wander, Power-line Interface, High-Frequency Noise).
  * Removed baseline wander with a high-pass filter (cutoff 0.5 Hz) — since this noise lives in very low frequencies, filtering those out leaves the ECG's real content untouched.
  * Removed power-line interference with a notch filter tuned precisely to 50 Hz — this deletes just that one frequency without disturbing anything else nearby.
  * Removed high-frequency noise with a low-pass filter (cutoff 40 Hz) — since real ECG content lives below that.
  * Detected R-peaks(the sharp spike in each heartbeat) using **findpeaks**.
  * Calculated heart rate from the average time gap between consecutive R-peaks.
* **Outputs:**
  * *Noisy signal plot* — The ECG buried under all three noise types simultaneously is messier than a clean heartbeat trace.
  <img width="460" height="276" alt="image" src="https://github.com/user-attachments/assets/de1ff5a9-40c2-4538-a725-89bd4bab8e6f" />

  * *Before/after comparison plot* — Shows the heartbeat shape emerging clearly once filtering is applied.
  <img width="460" height="276" alt="image" src="https://github.com/user-attachments/assets/d3466dd7-0fb8-4348-966e-8144efea7cfa" />

  * *Frequency spectrum comparison(before vs after)* — You can see the sharp spike at 50 Hz (power-line noise) and the low-frequency energy (baseline wander) present in the noisy spectrum vanish in the cleaned spectrum, while the ECG's actual frequency content stays intact.
  <img width="460" height="277" alt="image" src="https://github.com/user-attachments/assets/125ba083-8010-4ad3-a069-f3c7c73ea0bf" />

  * *R-peaks marked on the cleaned ECG* — 15 correctly detected peaks confirming the detection algorithm worked perfectly on the cleaned signal.
  <img width="460" height="276" alt="image" src="https://github.com/user-attachments/assets/ad5411e3-3ef6-45fe-a018-7aefb668a6b5" />

  * *Numeric results:*
    * 15 R-peaks detected — exactly matching the number of beats in the signal.
    * Average R-R interval: 0.800 s — matches exactly the 0.8-second beat spacing we built into the synthetic signal.
    * Estimated Heart Rate: 75.0 BPM — (60 seconds ÷ 0.8 s = 75), Confirming the whole pipeline — filtering, peak detection, and rate calculation — is correct.

* **Applications(Real World):**
  * *Hospital Diagnostic ECG Machines:* Cleaning raw clinical ECG readings by removing 50/60 Hz powerline interference (from wall outlets) and baseline drift (from patient breathing).
  * *Telemedicine & Remote Patient Care:* Cleaning digitized cardiac signals prior to data compression and transmission over low-bandwidth wireless networks.

* **Disadvantages:**
  * *Distortion of Critical Wave Features:* Traditional notch or linear low-pass filters can smooth out the high-frequency peaks of the R-peaks or distort the small P and T waves, leading to inaccurate medical diagnoses.
  * *Fixed Filter Inflexibility:* Static digital filters (like standard FIR/IIR filters) fail when noise characteristics change over time (e.g., when a patient moves suddenly or changes breathing patterns).

* **How To Fix Them:**
  * *Use Adaptive Filtering Algorithms:* Implement adaptive filters like Normalized Least Mean Squares (NLMS) or Recursive Least Squares (RLS) which self-adjust their filter coefficients dynamically based on changing noise levels.
  * *Combine Filtering Pipelines (Hybrid Approach):*
    * Use a Notch/Median Filter for low-frequency baseline drift.
    * Use Adaptive filtering for high-frequency muscle noise and powerline interference.

---
