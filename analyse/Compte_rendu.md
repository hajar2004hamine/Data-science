# HAMINE Hajar
<img src="image.jpeg" style="height:300px;margin-right:300px; float:left; border-radius:10px;"/>

**Numéro d'étudiant** : 22001267 
**Classe** : CAC2

---
# Compte rendu
## Analyse Prédictive de Régression sur Jeu de Données Reddit Sentiment Analysis

**Date :** 30 Novembre 2025

---

## Table des Matières

1.  [Introduction et Contexte](#1-introduction-et-contexte)
2.  [Analyse Exploratoire des Données](#2-analyse-exploratoire-des-données)
    * [Chargement et Structure du Dataset](#21-chargement-et-structure-du-dataset)
    * [Variable Cible et Variables Explicatives](#22-variable-cible-et-variables-explicatives)
    * [Encodage de la Variable Cible](#23-encodage-de-la-variable-cible)
    * [Statistiques et Visualisations](#24-statistiques-et-visualisations)
3.  [Méthodologie de Régression](#3-méthodologie-de-régression)
    * [Préparation des Données et TF-IDF](#31-préparation-des-données-et-tf-idf)
    * [Séparation Train/Test](#32-séparation-train-test)
    * [Modèles de Régression Testés](#33-modèles-de-régression-testés)
4.  [Résultats et Analyse Comparative](#4-résultats-et-analyse-comparative)
    * [Régression Linéaire Simple](#41-régression-linéaire-simple)
    * [Régression Polynomiale de Degré 2](#42-régression-polynomiale-de-degré-2)
    * [Régression par Arbre de Décision](#43-régression-par-arbre-de-décision)
5.  [Conclusion et Perspectives](#5-conclusion-et-perspectives)

---

## 1. Introduction et Contexte

Ce rapport présente une analyse prédictive réalisée sur un jeu de données textuelles issues de Reddit, annotées avec des sentiments (négatif, neutre, positif). L'objectif est de prédire un score numérique de sentiment après transformation des labels catégoriels, en utilisant des modèles de régression variés. Le projet illustre la difficulté de la régression sur données textuelles via des méthodes classiques.

---

## 2. Analyse Exploratoire des Données

### 2.1 Chargement et Structure du Dataset

Le dataset contient 31 948 observations réparties sur deux colonnes :

- `text` : textes des posts Reddit (texte libre).
- `label` : sentiment catégoriel (negative, neutral, positive).

Les deux colonnes sont de type chaîne de caractères.
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Chargement du dataset
df = pd.read_csv("reddit_sentiment_analysis.csv")  # adapte le chemin au besoin
print("Structure du dataset :")
print(df.info())
print("\nAperçu des premières lignes:")
print(df.head())
```

### 2.2 Variable Cible et Variables Explicatives

- Variable cible initiale : `label` catégorielle.
- Variables explicatives : contenu textuel à vectoriser pour modélisation.

### 2.3 Encodage de la Variable Cible

Pour rendre la tâche compatible avec des modèles de régression, la variable cible a été transformée par encodage numérique :

- negative → -1
- neutral → 0
- positive → 1

Une nouvelle colonne `sentimentscore` est créée avec ces valeurs numériques.
```python
sentiment_mapping = {"negative": -1, "neutral": 0, "positive": 1}
df["sentimentscore"] = df["label"].map(sentiment_mapping)
```

### 2.4 Statistiques et Visualisations

- Distribution des labels : 
  - Neutral : 19 728
  - Positive : 8 825
  - Negative : 3 395

- Aucune valeur manquante détectée.

- Les textes ont été vectorisés avec un **TF-IDF Vectorizer** limité à 5 000 caractéristiques pour gérer la haute dimensionnalité.
```python
plt.figure(figsize=(8,5))
sns.countplot(data=df, x='label', palette='Set2')
plt.title("Distribution des labels sentiments")
plt.xlabel("Label")
plt.ylabel("Nombre d'exemples")
plt.show()
```
---

## 3. Méthodologie de Régression

### 3.1 Préparation des Données et TF-IDF

Le texte brut est transformé en matrice numérique TF-IDF qui sert d'entrée aux modèles.
```python
from sklearn.feature_extraction.text import TfidfVectorizer

vectorizer = TfidfVectorizer(max_features=5000)
X_tfidf = vectorizer.fit_transform(df["text"])
y = df["sentimentscore"]
```

### 3.2 Séparation Train/Test

Les données ont été divisées en :

- Entraînement (80%)
- Test (20%)

avec un split aléatoire contrôlé pour validation robuste.
```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X_tfidf, y, test_size=0.2, random_state=42
)
```

### 3.3 Modèles de Régression Testés

- Régression linéaire simple
- Régression polynomiale de degré 2
- Régression par arbre de décision

Ces modèles permettent d'explorer la capacité à modéliser la relation entre le texte vectorisé et le score numérique de sentiment.

---

## 4. Résultats et Analyse Comparative
### 4.1 Régression Linéaire Simple

- Mean Squared Error (MSE) : environ 0.2321
- Coefficient de détermination (R²) : 0.3411

Le modèle linéaire explique environ 34% de la variance du score, indiquant une relation modérée mais insuffisante pour des prédictions précises.
```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

lr = LinearRegression()
lr.fit(X_train, y_train)
y_pred_lr = lr.predict(X_test)

mse_lr = mean_squared_error(y_test, y_pred_lr)
r2_lr = r2_score(y_test, y_pred_lr)

print(f"Régression Linéaire - MSE: {mse_lr:.4f}, R2: {r2_lr:.4f}")
```

### 4.2 Régression Polynomiale de Degré 2

- MSE amélioré à environ 0.2034
- R² augmenté à environ 0.4225

La prise en compte des termes quadratiques apporte une meilleure capture de la complexité non linéaire des données.
```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

poly = make_pipeline(PolynomialFeatures(degree=2), LinearRegression())
poly.fit(X_train, y_train)
y_pred_poly = poly.predict(X_test)

mse_poly = mean_squared_error(y_test, y_pred_poly)
r2_poly = r2_score(y_test, y_pred_poly)

print(f"Régression Polynomiale (deg2) - MSE: {mse_poly:.4f}, R2: {r2_poly:.4f}")
```

### 4.3 Régression par Arbre de Décision

- MSE plus élevé : 0.3845
- R² négatif : -0.0916 indiquant une performance inférieure à une prédiction moyenne.

Probable surapprentissage sans réglage fin des hyperparamètres ; pas adaptée à la nature très dispersée des caractéristiques TF-IDF.
```python
from sklearn.tree import DecisionTreeRegressor

dt = DecisionTreeRegressor(random_state=42)
dt.fit(X_train, y_train)
y_pred_dt = dt.predict(X_test)

mse_dt = mean_squared_error(y_test, y_pred_dt)
r2_dt = r2_score(y_test, y_pred_dt)

print(f"Régression Arbre de Décision - MSE: {mse_dt:.4f}, R2: {r2_dt:.4f}")
```
```python
| Modèle                           | MSE    | R² Score |
| -------------------------------- | ------ | -------- |
| Régression Linéaire Simple       | 0.2321 | 0.3411   |
| Régression Polynomiale (Degré 2) | 0.2034 | 0.4225   |
| Arbre de Décision                | 0.3845 | -0.0916  |
```

## 5. Conclusion et Perspectives

Cette étude montre que la régression prédictive sur un dataset textuel avec des modèles classiques est un défi :

- Les modèles simples capturent une partie des tendances mais restent limités.
- La régression polynomiale montre une amélioration notable, mais le score R² reste modeste.
- L'arbre de décision sans optimisation est inadapté dans ce contexte.
- Pour améliorer les performances, il est recommandé d'explorer des techniques avancées de traitement du langage naturel (NLP), telles que des embeddings pré-entraînés (Word2Vec, GloVe), des réseaux neuronaux (RNN, LSTM, Transformers) ou des modèles d'ensemble sophistiqués (Gradient Boosting, Random Forests optimisés).

Ce document illustre la démarche complète : exploration, prétraitement, modélisation et évaluation dans un cadre de régression sur données textuelles.

---




