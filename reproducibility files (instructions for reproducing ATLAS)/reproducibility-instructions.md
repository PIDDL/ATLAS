# 🔍 Reproducibility - ATLAS

This guide provides detailed instructions for reproducing **ATLAS**, including setting up the environment, organizing folders, and running the system. 

📌 **Repository:** Clone the ATLAS repository from GitHub:
```sh
git clone https://github.com/purseclab/ATLAS
```
🚀 Follow the steps below to ensure all dependencies are installed, folders are correctly structured, and results are accurately reproduced.

---

# 🛠 Setting Up the Environment

## **Option 1: Using Python Virtual Environment**
1️⃣ **Install Python 3.7.7** from the [official Python website](https://www.python.org/downloads/).  

2️⃣ **Create a Virtual Environment:**
```sh
python3.7 -m venv venv
```

3️⃣ **Activate the Virtual Environment:**
- **On Windows:**  
  ```sh
  venv\Scripts\activate
  ```
- **On Linux/Mac:**  
  ```sh
  source venv/bin/activate
  ```

4️⃣ **Install Dependencies:**
```sh
pip install tensorflow==2.3.0 keras==2.4.3 fuzzywuzzy==0.18.0
pip install matplotlib==2.2.5 numpy==1.16.6 networkx==2.2
```

---

## **Option 2: Using Docker (Recommended)**
To create a **Docker container**, follow these steps:

### **1️⃣ Build the Docker Image**
```sh
docker build -t atlas_env .
```

### **2️⃣ Run the Container**
```sh
docker run -it --mount type=bind,source=$(pwd)/datasets,target=/app/datasets atlas_env
```
📌 **Note:** This mounts your local dataset folder inside the container.

---

# 📂 Setting Up the Folders

## **General Steps (For All Experiments)**
1. Open the `paper_experiments` folder and unzip all experiment folders (`S1-S4` and `M1-M6`).
2. Copy all unzipped experiment folders into the **root ATLAS** folder.
3. For each experiment folder (`S1-S4`, `M1-M6`), delete the following subfolders:
   - `output`
   - `training_logs`
   - `testing_logs`
   - `resampling`
4. Navigate to the `raw_logs` folder inside `ATLAS`, and unzip all folders corresponding to each experiment.

---

# 🚀 Running ATLAS

### **A) Preprocess the Logs**
```sh
python preprocess.py
```
This generates a **preprocessed log file** for each log folder in `training_logs` and `testing_logs`.

### **B) Generate Graph Files**
```sh
python graph_generator.py
```
This processes preprocessed logs and generates **graph files**.

### **C) Generate Sequence Files**
```sh
python graph_reader.py
```
This processes **graph files** into **sequence (text) files**.

---

# 🔥 Running ATLAS - Training & Testing

## **Step 1: Generate Resampled Files**
Edit `atlas.py`:
```python
DO_TRAINING = True
load_resampling = False
load_nonsampling = False
load_undersampling = False
```
Run:
```sh
python atlas.py
```

## **Step 2: Train the Model**
Edit `atlas.py`:
```python
DO_TRAINING = True
load_resampling = True
```
Run:
```sh
python atlas.py
```
🔹 After training, `model.h5` will be saved in the `output` folder.

## **Step 3: Test the Model**
Edit `atlas.py`:
```python
DO_TRAINING = False
```
Run:
```sh
python atlas.py
```
🔹 Predicted attack entities will be displayed on the terminal.

---

# ✨ **Cleaning Predicted Entities (Before Evaluation)**
Once testing is complete, **you need to clean the predicted entities manually** before evaluating.

### **Steps to Clean the Predicted Entities:**
1. **Copy the predicted entities** from the terminal output.
2. **Remove redundant entities**  
   - Example: `"payload.exe"` and `"payload.exe_892"` refer to the same file. Keep only `"payload.exe"`.
3. **Add related entities manually (if needed)**  
   - Example: If `"0xalsaheel.com"` is reported, also include its resolved IP `"192.168.223.3"`.
4. **Final cleaned output should look like this:**
   ```json
   ["0xalsaheel.com", "aalsahee/index.html", "192.168.223.3", "payload.exe"]
   ```

---

# 🔍 Evaluating the Model

After testing, a JSON file starting with `eval_` will be generated in `output/`.

1. **Open the JSON file** and replace the first `[]` with the cleaned predicted entities:
   ```json
   ["0xalsaheel.com", "aalsahee/index.html", "192.168.223.3", "payload.exe"]
   ```
2. If this result is for a host (e.g., h1) in a **multi-host** attack scenario (e.g., M1), then copy the JSON file to the "output" folder in the second host folder (e.g., h2), this way when we run the evaluate.py program (in h2 folder) it will consider all involved hosts. 

3. **Run Evaluation Script:**
   ```sh
   python evaluate.py
   ```

---

# 🐳 Running ATLAS Inside Docker

### **1️⃣ Build the Docker Image**
```sh
docker build -t atlas_env .
```

### **2️⃣ Run the Container**
```sh
docker run -it --mount type=bind,source=$(pwd)/datasets,target=/app/datasets atlas_env
```
*(Mounts local datasets inside the container.)*

### **3️⃣ Activate the Conda Environment**
```sh
/opt/conda/bin/conda run -n atlas_env bash
```

### **4️⃣ Run ATLAS Scripts**
```sh
python preprocess.py
python graph_generator.py
python graph_reader.py
python atlas.py
python evaluate.py
```

📌 **Note:** If cloning fails using **HTTPS**, try using **SSH**:
```sh
git clone git@github.com:purseclab/ATLAS.git
```
Ensure **SSH keys** are configured for GitHub.

---

# ⚠ Important Notes
✅ Repeat steps for **each experiment (`S1-S4`, `M1-M6`)**  
✅ Update variables in `atlas.py` correctly before **each phase (resampling, training, testing)**  
✅ **Always clean the predicted entities manually** for accurate results  
✅ **Docker users:** Ensure volumes are correctly mounted  

---

### **🎯 Conclusion**
Following these steps will help **reproduce ATLAS successfully**. Use the **Docker method** for an isolated, reproducible setup.