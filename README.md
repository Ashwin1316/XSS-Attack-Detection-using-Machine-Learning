# XSS Attack Detection using Machine Learning

## Objective
The objective of this project is to detect malicious Cross-Site Scripting (XSS) payloads using a hybrid Machine Learning approach. By analyzing text inputs for suspicious patterns (like Javascript events, script tags, and special characters) and combining those with TF-IDF word vectors, the model accurately classifies whether an input is a safe text or a cyberattack.

## Folder Structure
```text
XSS-DS-Jupyter/
│
├── Dataset/
│   └── XSS_dataset.csv          # The balanced dataset with 13,686 XSS and benign payloads
│
├── Notebook/
│   ├── Untitled.ipynb           # Original Jupyter Notebook for research and visualization
│   ├── train_model1.py          # Modularized, production-ready training script
│   ├── predict.py               # Testing script to input strings and get predictions
│   ├── xss_hybrid_model.pkl     # Saved VotingClassifier model (generated after training)
│   ├── tfidf.pkl                # Saved TF-IDF Vectorizer
│   └── scaler.pkl               # Saved StandardScaler
│
├── requirements.txt             # Python dependencies
├── README.md                    # Project documentation
└── Viva_Explanation.md          # Guide for explaining the project to professors
```

## Technologies Used
- **Python 3**
- **Data Manipulation:** `pandas`, `numpy`
- **Visualization:** `matplotlib`, `seaborn`
- **Machine Learning Extraction:** `scikit-learn` (TF-IDF, StandardScaler)
- **Algorithms:** `SVC`, `XGBoost`, `LightGBM`, `CatBoost`

## Installation Steps
1. Open your terminal in the root folder (`XSS-DS-Jupyter`).
2. Create a virtual environment:
   ```powershell
   python -m venv venv
   ```
3. Activate the virtual environment:
   ```powershell
   .\venv\Scripts\Activate.ps1
   ```
4. Install all dependencies:
   ```powershell
   pip install -r requirements.txt
   ```

## How to Run

### 1. Training the Model
If you want to train the model from scratch, activate your environment, move into the `Notebook` folder, and run the training script:
```powershell
.\venv\Scripts\Activate.ps1
cd Notebook
python train_model1.py
```
*This will clean the dataset, extract features, train the ensemble algorithm, print evaluation metrics, and save `.pkl` files to your disk.*

### 2. Testing / Making Predictions
To see the AI in action and test custom payloads, run the prediction script from the `Notebook` folder:
```powershell
.\venv\Scripts\Activate.ps1
cd Notebook
python predict.py
```

## Expected Output
When running `predict.py`, you will see instant classification.
- **Input:** `<script>alert('You have been hacked!');</script>`
- **Output:** `>> RESULT: 🚨 MALICIOUS (XSS Attack Detected!)`

- **Input:** `Hello world, this is a normal comment!`
- **Output:** `>> RESULT: ✅ SAFE (Clean Text)`
