# Project Viva Explanation Guide

If your professor asks you to explain this project, use this simple guide to sound confident and professional!

## 1. "What is the objective of your project?"
**Your answer:**
"The goal of this project is to build a Machine Learning model that automatically detects **Cross-Site Scripting (XSS)** attacks. XSS happens when a hacker tries to inject malicious JavaScript into web forms or URLs. Our AI reads the text input and instantly classifies it as either `Safe (0)` or `Malicious (1)`."

## 2. "What dataset did you use and how did you preprocess it?"
**Your answer:**
"We used an open-source dataset containing about 13,600 payloads. It was well-balanced with about 54% malicious and 46% safe samples. 
For preprocessing, we first cleaned the text:
1. Converted everything to lowercase.
2. Removed standard URLs (since they are usually safe noise).
3. Stripped out unnecessary special characters (but intentionally kept characters like `<`, `>`, `/`, `=`, heavily used in XSS).
4. **Most importantly:** We dropped over 2,700 duplicates to prevent data leakage so our model wouldn't just memorize the answers."

## 3. "What features did you extract from the text?"
**Your answer:**
"We didn't just give raw text to the model. We engineered a combination of manual features and automated features:
- **Manual Features:** We wrote code to count the length of the string, the exact number of `<script>` tags, the number of JavaScript event handlers (like `onmouseover`), and the density of special characters.
- **Automated Features:** We used **TF-IDF** (Term Frequency-Inverse Document Frequency) to extract the top 100 most important vocabulary words used across the payloads.
We then combined these arrays and scaled them using a `StandardScaler`."

## 4. "Which Machine Learning algorithms did you use?"
**Your answer:**
"We initially experimented with `SVC` (Support Vector Classifier), but our final and best model is a **Hybrid Ensemble Model**. 
We combined three state-of-the-art Gradient Boosting algorithms:
1. **XGBoost**
2. **LightGBM**
3. **CatBoost**

We put them inside a `VotingClassifier` using 'soft' voting. This means the three algorithms average their exact probability scores together to make a final super-accurate prediction."

## 5. "How do you know your model is good? What were the results?"
**Your answer:**
"We split our data 80/20. We trained on 80% and tested on 20% unseen data. Because our dataset was balanced, we didn't just look at Accuracy; we evaluated Precision, Recall, and the F1-Score. The ensemble model scored near-perfect across all metrics, proving it learned the underlying patterns of XSS rather than just memorizing strings."

## 6. "How is the project structured?"
**Your answer:**
"We separated our workflow perfectly. We did our initial data analysis in Jupyter Notebook (`Untitled.ipynb`). But for the final software, we modularized the code into `train_model1.py` which trains and saves the model to disk (as `.pkl` files). Finally, we created `predict.py` which loads the brain from the disk and allows us to verify and classify any new string instantly!"
