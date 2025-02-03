# **ATLAS Reproducibility Issues & Fixes**

## **📌 Overview**  
This document compiles all **reproducibility issues** encountered while running **ATLAS end-to-end** and their respective solutions (if available). The goal is to ensure consistency between the obtained results and the **author’s expected results**, while addressing challenges faced during preprocessing, training, testing, and evaluation.

---

## **🛑 Issues & Fixes**

### **1️⃣ Getting 0 False Positives (FP) and 0 False Negatives (FN) in Evaluation**
- **Issue:**  
  - Despite using the **preprocessed logs**, **resampled dataset**, and **trained model**, the evaluation consistently showed **0 FP and 0 FN**.  
  - This indicated a discrepancy between **predicted entities** and the expected ground truth.

- **Resolution:**  
  - **Copied the predicted entities** from the terminal output after running ATLAS for testing.  
  - **Manually cleaned** the predicted entities following the **instructions provided in the author's README**.  
  - Re-ran the evaluation after cleaning, leading to more meaningful results.

---

### **2️⃣ Differences in Predicted Entities Compared to the Author's Results**
- **Issue:**  
  - The number of **predicted entities** in my evaluation was **higher than the author’s**, indicating potential overprediction.  
  - My model assigned **higher probabilities to predicted entities**, suggesting differences in **data preprocessing** or **model training**.  

- **Note:** No specific resolution identified yet.

---

### **3️⃣ Different Resampled Dataset File Sizes & Training Time**
- **Issue:**  
  - The **file size of the resampled dataset** was different from the author's.  
  - This led to **faster training time** on my end.  

- **Note:** No direct resolution identified yet.

---

### **4️⃣ Parsing Issue with DOT Files**
- **Issue:**  
  - Errors were encountered while parsing DOT files during graph generation.  
  - The issue resulted in incomplete sequence graphs.

- **Resolution:**  
  - Used **Jaffer’s repository files**, which resolved the parsing issue.  
  - Ensured that **graph files were generated correctly** before proceeding with further steps.

---

### **5️⃣ Unclear Folder Structure and File Usage**
- **Issue:**  
  - The **`paper_experiments`** folder contains the author's results for each experiment but **does not explain** the required structure for reproduction.  
  - Lack of clarity in how files should be organized before running ATLAS.

- **Resolution:**  
  - Followed the structure from **`paper_experiments`**, ensuring **consistency with the provided results**.  
  - Matched **training and testing logs structure** to align with the author's expected dataset organization.

---

### **6️⃣ Multiple `malicious_labels` Files for One Log**
- **Issue:**  
  - Found **multiple `malicious_labels` files** for the same log in several training log folders.  
  - Example: In **training logs of S1 in S2**, different versions of the file were present:  
    ```
    malicious_labels
    malicious_labels (copy)
    malicious_labels (another copy)
    ```
  - This caused confusion in selecting the correct file for processing.

- **Resolution:**  
  - Chose the file **named exactly** as `malicious_labels`.  
  - **Ignored duplicate versions** like `malicious_labels (copy)` or `malicious_labels (another copy)`.  
  - Ensured **consistent selection across all training log folders** to match the expected dataset structure.

---

## **🔍 Summary of Fixes**
| Issue | Resolution |
|-------|-----------|
| **0 FP & 0 FN in Evaluation** | Manually cleaned predicted entities as per the author's README. |
| **Parsing Issue with DOT Files** | Used Jaffer’s files to resolve graph generation errors. |
| **Unclear Folder Structure** | Followed `paper_experiments` structure for proper dataset alignment. |
| **Multiple `malicious_labels` Files** | Used only the original `malicious_labels` file, ignoring copies. |

---

