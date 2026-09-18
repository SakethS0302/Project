## 5. DTMF Tone Detection

---
* **Description:** Dual-Tone Multi-Frequency(DTMF) decoding system to translate telephone keypad sounds into their corresponding numbers.
* **What We Did:**
  * Understood the encoding scheme by pairing one from a "low" frequency group(697, 770, 852, or 941 Hz — the rows) and one from a "high" frequency group(1209, 1336, 1477, or 1633 Hz — the columns).
  * Generated a test signal by encoding the sequence 1470*8#D as genuine DTMF tones(each digit as its correct frequency pair) with brief silences between key presses, just like an actual phone dial would sound.
  * Segmented the audio by separating the continuous audio into 8 individual key-press segments (ignoring the silent gaps between them).
  * Applied FFT for every isolated tone and computed its frequency spectrum at each of the 8 known DTMF frequencies.
  * Whichever low frequency and whichever high frequency had the most energy, in combination, mapped back to one specific key via a lookup table matching the standard telephone keypad layout.
  * Verified correctness by comparing the original encoded sequence against what the system decoded.

* **Outputs:**
  * For every single tone, the system correctly identified both frequencies and the resulting digit.
    * Segment 1: low = 697 Hz, high = 1209 Hz -> digit "1"
    * Segment 2: low = 770 Hz, high = 1209 Hz -> digit "4"
    * Segment 3: low = 852 Hz, high = 1209 Hz -> digit "7"
    * Segment 4: low = 941 Hz, high = 1336 Hz -> digit "0"
    * Segment 5: low = 941 Hz, high = 1209 Hz -> digit "*"
    * Segment 6: low = 852 Hz, high = 1336 Hz -> digit "8"
    * Segment 7: low = 941 Hz, high = 1477 Hz -> digit "#"
    * Segment 8: low = 941 Hz, high = 1633 Hz -> digit "D"

  * For each tone, two sharp, distinct peaks are visible (marked in the plot) at exactly the row and column frequencies.
  <img width="460" height="276" alt="image" src="https://github.com/user-attachments/assets/d3081f83-872d-4ce7-8cad-0cf152714573" />
  <img width="460" height="277" alt="image" src="https://github.com/user-attachments/assets/baa52bd7-2f2b-4245-9c92-dcaae57cc116" />

  * The decoded output exactly matches what was originally encoded, with zero errors across all 8 digits, including the non-numeric keys.

* **Applications(Real World):**
  * *Interactive Voice Response(IVR) Systems:* Phone banking, automated customer support, and call center menus that process touch-tone keypad inputs to navigate options (e.g., "Press 1 for Sales, Press 2 for Support").
  * *Remote Control & Industrial Automation:* Controlling remote hardware, gate openers, or radio repeaters over voice channels using specific keypad tone combinations.
  * *Telecommunications Switching & Signaling:* Transmitting dialed numbers over traditional analog landlines to route phone calls through central exchanges.

* **Disadvantages:**
  * *Sensitivity to Acoustic & Transmission Noise:* Background speech, line hum, or severe line attenuation can mask frequencies, causing missed keypresses.
  * *Computational Cost of Full FFT:* Running a full Fast Fourier Transform(FFT) calculates unnecessary frequencies across the entire spectrum when only 8 specific DTMF frequencies are needed.

* **How To Fix Them:**
  * *Apply Bandpass Pre-Filtering:* Filter out frequencies below 300 Hz and above 3400 Hz using digital bandpass filters before decoding to eliminate speech interference and out-of-band noise.
  * *Framing & Windowing Optimization:* Use overlapping short sliding windows(10 – 20 ms) to reliably detect short keypresses without skipping frames.

---
