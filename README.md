# 🎵 TikTok Content Moderation & Claim Classification Project

> **Professional Data Science Portfolio Project** developed by **Automatidata** in collaboration with TikTok’s Data & Safety Team.

---

## 📊 Data Source

* **Dataset:** TikTok Claims Classification Dataset (*Google Advanced Data Analytics Certificate*)
* **Source:** Synthetically generated dataset provided by Google for learning and portfolio demonstration purposes.
* **Description:** Includes user-reported video data with features such as video claim status, view counts, likes, shares, downloads, author verification status, and video duration.

> **Note:** This dataset was created specifically for this course capstone project and does not represent real-world internal TikTok company data.

---

## 📌 Project Overview
The primary objective of this project is to build data-driven predictive models that assist TikTok’s Trust & Safety team in classifying user video submissions as either **claims** or **opinions**. 

By automatically identifying claim-based content—which carries a higher risk of containing misinformation or requiring policy moderation—TikTok can optimize human moderation queues, reduce review backlogs, and streamline creator verification workflows.

---

## 🗂️ Repository Structure

```text
tiktok-project/
│
├── Notebooks/
│   ├── 01_EDA_and_Inspection.ipynb
│   ├── 02_Hypothesis_Testing.ipynb
│   ├── 03_Statistical_Review.ipynb
│   ├── 04_Logistic_Regression.ipynb
│   └── 05_Machine_learning.ipynb
│
├── Reports/
│   ├── Executive_Summary_TikTok_EDA_and_Hypothesis_Testing.docx
│   ├── Executive_Summary_TikTok_Logistic_Regression.docx
│   └── Executive_Summary_TikTok_Machine_Learning.docx
│
└── README.md

```
---

## 📊 Key Insights & Model Performance

### 1. Exploratory Data Analysis & Statistical Review
* **Content Type Disparity:** Analyzed 19,382 video records. Verified accounts predominantly author opinion content, whereas unverified creators generate the vast majority of claim videos.
* **Data Quality & Skewness:** Handled right-skewed interaction distributions and addressed missing values across engagement variables (`video_view_count`, `video_like_count`, `video_share_count`).
* **Statistical A/B Testing:** Conducted two-sample hypothesis testing on video view counts across author verification statuses. Proved a statistically significant difference ($p < 0.05$) in engagement between verified and unverified accounts.

### 2. Logistic Regression (Verified Status Prediction)
* **Statistical Inference:** Built a binary logistic regression model to evaluate how engagement metrics and video claim status influence account verification (`verified_status`).
* **Dominant Feature:** Identified `claim_status_opinion` as the primary driver—posting an opinion increases the odds of an account being verified by **> 100x** compared to posting a claim, holding engagement constant.
* **Model Baseline Performance:** $F_1\text{-score} = 0.63$ | $\text{Recall} = 0.65$ | $\text{Precision} = 0.61$ | $\text{Accuracy} = 0.65$.

### 3. Machine Learning Classification (Claim vs. Opinion)
* **Target Classification:** Built supervised tree-based ensemble models (Random Forest and XGBoost) to classify whether a video is a `claim` or an `opinion`.
* **Champion Model:** **Random Forest Classifier** achieved $0.99$ accuracy, precision, recall, and F1-score on the test dataset.
* **Feature Importance Insights:** Engagement interaction metrics (`video_view_count`, `video_like_count`, `video_share_count`) and transcription character lengths served as primary split variables in tree ensembles.

---

## 📈 Model Evaluation Summary

Quantitative evaluation metrics across evaluated classification models:

| Model Architecture | Target Variable | Precision | Recall | F1-Score | Accuracy | Status |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: |
| **Logistic Regression** | `verified_status` | 0.61 | 0.65 | 0.63 | 0.65 | Inference Baseline |
| **Random Forest Classifier** | `claim_status` | **0.99** | **1.00** | **0.99** | **0.99** | **Champion Model** |
| **XGBoost Classifier** | `claim_status` | 0.99 | 0.99 | 0.99 | 0.99 | High-Performance Benchmark |

> **Champion Model Verdict:** **Random Forest** is selected as the production champion model due to its optimal balance of predictive accuracy ($0.99$), robustness against overfitting, and high stability across validation splits.

---

## 💡 Strategic Recommendations & Operational Roadmap

* **Upstream Triage Pipeline Integration:** Deploy the **Random Forest Champion Model** as an automated first-line triage filter to categorize incoming video submissions in real time.
* **Account Verification Policy:** Integrate claim status into creator verification workflows. Creators posting original opinion content with high engagement should be routed to expedited verification tracks.
* **Misinformation Safeguards:** Unverified accounts posting claims that trigger rapid engagement spikes should be flagged for proactive policy review prior to recommendation engine amplification.
* **Hybrid Human-in-the-Loop Review:** Route borderline classification cases to human moderation teams, focusing manual oversight on high-risk claims with viral engagement.
* **Continuous Monitoring:** Implement periodic retraining routines to account for evolving creator slang, transcript length variations, and shifting platform trends.

---

## 🛠️ Tech Stack & Libraries
* **Python** 🐍
* **Data Manipulation & Analysis:** Pandas, NumPy
* **Machine Learning & Modeling:** Scikit-Learn (Logistic Regression, Random Forest, GridSearchCV, Cross-Validation), XGBoost
* **Statistical Analysis:** SciPy (Two-sample t-tests, Welch's t-test)
* **Visualization:** Matplotlib, Seaborn
* **Environment:** Jupyter Notebooks
