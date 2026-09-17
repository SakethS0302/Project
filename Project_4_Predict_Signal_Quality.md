# 4. Predict Signal Quality

---
* **Description:** Evaluated wireless channel performance under dynamic, real-world noise and interference conditions to predict signal degradation and optimize communication reliability.
* **What We Did:**
  * Generated and tested 600 signals(150 each) at four known noise severities: SNR = 20 dB (barely noisy), 10 dB, 5 dB, and 0 dB (noise as strong as the signal itself).
  * Extracted 8 DSP features per noisy signal instead of feeding raw samples to the network which changes as noise increases.
  * Trained an ANN regression model with two hidden layers using Fitnet to map those 8 features which uses 80% of the data for training/validation and holds back 20% purely for testing.
  * Evaluated on unseen test data to see how close the predicted SNR came to the true SNR.

* **Outputs:**
  * *Test RMSE: 0.00 dB and Test MAE: 0.00 dB* — The network's predictions were so close to the true SNR values that the error rounds to zero at 2 decimal places.
  <img width="460" height="277" alt="image" src="https://github.com/user-attachments/assets/2a43c644-6e0a-4c7d-898a-36a574511bb4" />

  * *Regression plot* — MATLAB's built-in correlation plot, which should show an R-value equal to 1(perfect linear correlation between predicted and true SNR).
  <img width="626" height="626" alt="image" src="https://github.com/user-attachments/assets/c8993426-19ea-45c9-8237-e7b71c4f1e86" />

  * *Prediction Error Distribution* - Indicates a well-fitted model with zero prediction error across almost all tested samples.
  <img width="460" height="276" alt="image" src="https://github.com/user-attachments/assets/66bb6804-3f5c-4450-939d-42b9c1a62195" />

* **Applications(Real World):**
  * *Satellite & Space Communications* - Ground stations continuously evaluate link quality and atmospheric attenuation to optimize power allocation and prevent data packet loss during satellite passes.
  * *5G/6G Adaptive Modulation & Coding (AMC)* - Cellular towers predict channel degradation in real time to adjust data transmission rates and modulation schemes to maintain stable connections.

* **Disadvantages:**
  * *High Computation Overhead:* Complex predictive algorithms(like Deep learning models) require processing power, which can introduce latency in real-time edge devices.
  * *Over-reliance on Statistical Assumptions:* Many standard quality estimation models assume static Additive White Gaussian Noise (AWGN), failing when confronted with sudden burst noise or multi-path fading.

* **How To Fix Them:**
  * *Feature Extraction & Hybrid Noise Modeling:* Incorporate multi-path fading models like Rayleigh fading into the training dataset alongside AWGN to improve real-world model accuracy.
  * *Implement Adaptive Extended Kalman Filters:* To continuously track time-varying channel parameters with low computational complexity.

---
