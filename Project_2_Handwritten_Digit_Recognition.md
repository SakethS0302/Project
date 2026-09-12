# 2. Handwritten Digit Recognition

---
* **Description:** Pattern recognition and classification model designed to identify handwritten digits from image datasets.
* **What We Did:**
  * Got 5000 labelled data as images for training and 5000 for testing.
  * Built a network with 784 input pixels, 2 Hidden layers(128 Neurons, then 64 Neurons) and 10 neurons in the output layer.
  * Trained it by repeatedly showing it labeled examples, letting it guess, measuring how wrong the guess was, and adjusting internal weights via backpropagation to reduce that error.
  * Tested it on the 5,000 images it had never seen during training.
* **Outputs:**
  * *96% test accuracy* — The network correctly identified the digit in about 4,800 out of 5,000 unseen images.
  <img width="460" height="276" alt="image" src="https://github.com/user-attachments/assets/92810f22-aca6-4033-80ed-5d1a685eab21" />
  
  * *Training converged cleanly* — The Performance and Training State plots showed error steadily dropping and gradients shrinking, with validation error tracking training error well.
  * The Error Histogram showed most predictions were confidently correct, with only a small tail of genuinely wrong guesses.
  * the Confusion Matrix let us see which digits got mixed up with which (commonly digits that look visually similar when handwritten, like 4/9 or 3/8).
  <img width="1920" height="992" alt="image" src="https://github.com/user-attachments/assets/bdd62ed8-3a68-4158-a19a-bb2a715afc2c" />
  <img width="460" height="276" alt="image" src="https://github.com/user-attachments/assets/5cc82563-574b-41a4-8c5d-54a32ba4f9d0" />

* **Applications:(Real World)**
  * *Automated Check & Banking Document Processing*
    * Form Digitization: Financial institutions automatically extract account numbers, phone numbers, and Social Security numbers from hand-filled paper applications.
  * *Automated Exam Scoring & Form Processing*
    * OMR & Answer Sheet Scanning: Educational institutions scan handwritten student IDs, roll numbers, and numerical test answers on standardized exams, processing thousands of forms per minute.
  * *Healthcare & Medical Record Digitization*
    * Clinical Notes & Prescription Processing: Hospitals convert handwritten patient charts, dosages, and numerical vital statistics into electronic health records (EHRs).

* **Disadvantages:**
  * *Font and Handwriting Style Variance:* Simple classifiers (like basic K-NN or Linear SVMs) fail when encountering unique slant, stroke thickness, or unconventional writing styles.
  * *Sensitivity to Orientation and Scale:* Basic pixel-based inputs struggle if digits are rotated, scaled down, or shifted off-center within the image frame.

* **How to Fix them:**
  * *Data Augmentation:* Artificially expand your training set by applying random rotations, scaling, translations, and adding mild Gaussian noise to force the model to learn invariant features.
  * *Preprocessing & Binarization:* Apply morphological operations (erosion/dilation) to normalize stroke thickness and clean background noise before classification.

* **Alternative Datasets:**
  * *MNIST (Standard Baseline)*
    * Characteristics - 70,000 clean, centered, grayscale 28 x 28 images of isolated digits (0–9).
    * Results - High Accuracy(98%-99.5%); Ideal baseline.
  * *USPS Dataset*
    * Characteristics - 9,298 low-resolution(16 x 16) scanned digits from envelope mail processed by the US Postal Service.
    * Results - Moderate Accuracy(90%-95%); Blurrier images test model robustness against low resolution and varied compression artifacts.

---
