# 🍽️ Recipe Cuisine Classification Using NLP

An academic NLP project that classifies the **cuisine of a recipe based on its ingredients** using TF-IDF and Linear Support Vector Machine (SVM).

## 📌 Project Overview

Recipes from different cuisines often share common ingredients, making automatic cuisine classification a challenging NLP problem.

This project uses ingredient lists as textual data and builds a machine learning classification pipeline to predict the cuisine of a recipe.

The project is inspired by the 2014 research paper **“Automatic Recipe Cuisine Classification by Ingredients.”**

## 📚 Research Paper Approach

The research paper explored cuisine classification using ingredient information.

The main approach included:

* Boolean ingredient representation
* Ingredient presence/absence as features
* Support Vector Machine (SVM) classification
* Associative Classification
* SVM combined with SVD

The paper reported SVM accuracies for six cuisines:

| Cuisine  | Accuracy |
| -------- | -------: |
| Chinese  |      74% |
| German   |      89% |
| Italian  |      71% |
| Japanese |      74% |
| Spanish  |      83% |
| Thai     |      81% |

Our project does **not directly implement the paper's Boolean SVM approach**. Instead, it develops an improved TF-IDF-based representation.

## 🧠 Our Approach

The project follows this workflow:

```text
Recipe Dataset
      ↓
Ingredient Preprocessing
      ↓
Lowercase & Cleaning
      ↓
Preserve Multi-word Ingredients
      ↓
80/20 Stratified Train-Test Split
      ↓
Baseline: TF-IDF + Linear SVM
      ↓
Improved Ingredient-aware TF-IDF
      ↓
Linear SVM + GridSearchCV
      ↓
Final Evaluation
      ↓
Cuisine Prediction
```

### Ingredient Preprocessing

Ingredients are:

* Converted to lowercase
* Cleaned of unnecessary characters
* Converted into a consistent text representation
* Multi-word ingredients are preserved as meaningful units

For example:

```text
soy sauce → soy_sauce
olive oil → olive_oil
basmati rice → basmati_rice
```

This helps the model distinguish meaningful ingredient combinations rather than treating each word independently.

## 📊 Dataset

The project uses the **Kaggle Recipe Ingredients (What's Cooking)** dataset.

* **Total recipes:** 39,774
* **Training samples:** 31,819
* **Testing samples:** 7,955
* **Features:** `id`, `cuisine`, `ingredients`
* **Train/Test split:** 80/20
* **Stratification:** Yes
* **Random state:** 42

## 🤖 Models

### Baseline

**TF-IDF + Linear SVM**

Baseline accuracy:

**76.42%**

This serves as the reference point for measuring the improvement.

### Improved Model

The improved approach uses:

**Ingredient-aware TF-IDF + Linear SVM**

GridSearchCV was used to tune the SVM parameter `C`.

Parameters tested:

```text
C = [0.1, 1, 10]
```

* Cross-validation: 5-fold Stratified CV
* Best C: **1**
* Best cross-validation accuracy: **78.17%**
* Final vocabulary size: **6,313**

## 📈 Final Results

The final tuned model achieved:

| Metric             |      Score |
| ------------------ | ---------: |
| Accuracy           | **78.39%** |
| Weighted Precision | **78.01%** |
| Weighted Recall    | **78.39%** |
| Weighted F1-Score  | **77.98%** |

### Baseline vs Improved

| Model                 |   Accuracy |
| --------------------- | ---------: |
| Baseline TF-IDF + SVM |     76.42% |
| Improved + Tuned SVM  | **78.39%** |

**Improvement: +1.97 percentage points**

## 🔎 Prediction Demo

The final model can classify a new recipe from its ingredient list.

The prediction system displays the **top 4 cuisine confidence scores**, with the cuisine having the highest score selected as the final prediction.

> The displayed percentages are normalized SVM confidence scores and should not be interpreted as calibrated probabilities.

### Example

```text
Ingredients:
basmati rice, chicken, yogurt, garam masala,
turmeric, cumin, coriander, ginger, garlic, onion

Predicted Cuisine:
INDIAN
```

## ⚠️ Model Limitation

The model can struggle when cuisines have overlapping ingredient patterns.

A demonstrated failure case:

```text
Actual Cuisine: Vietnamese
Predicted Cuisine: Thai
Top Confidence Score: 28.54%
```

Ingredients:

```text
rice noodles
fish sauce
lime
mint
cilantro
bean sprouts
chili
```

This shows that ingredient-based representations may have difficulty distinguishing cuisines with similar ingredients and flavor profiles.

## 📌 Key Findings

* Ingredient lists can be effectively treated as NLP text for cuisine classification.
* The baseline TF-IDF + Linear SVM achieved **76.42% accuracy**.
* Preserving multi-word ingredients improved the representation.
* GridSearchCV helped select the best SVM parameter.
* The final model achieved **78.39% accuracy**.
* The model improved the baseline by **1.97 percentage points**.
* Overlapping ingredients remain a major source of classification errors.

## 🚀 Future Scope

Possible improvements include:

* Richer ingredient and contextual representations
* Larger and more balanced datasets
* Better handling of overlapping ingredients
* Advanced NLP and deep-learning models
* Contextual embeddings for ingredient descriptions

## 🛠️ Technologies Used

* Python
* Pandas
* NumPy
* Scikit-learn
* TF-IDF
* Linear SVM
* GridSearchCV
* Matplotlib
* Seaborn
* Google Colab
* KaggleHub

## 📁 Project Structure

```text
Recipe-Cuisine-Classification/
│
├── cuisine_sense.ipynb
├── README.md
└── MCA_Project_Template.pptx
```

## 📖 Reference

**Automatic Recipe Cuisine Classification by Ingredients (2014)**

This project uses the research paper as the conceptual foundation while implementing an improved TF-IDF and Linear SVM based approach.

## 👩‍💻 Project

Academic MCA NLP Project
**Cuisine Sense - Recipe Cuisine Classification Using NLP**
