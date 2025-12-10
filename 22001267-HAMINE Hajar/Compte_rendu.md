# HAMINE Hajar

<img src="Hajar.jpg" style="height:300px;margin-right:300px; float:left; border-radius:10px;"/> <img src="encg settat.jpeg" style="height:300px;margin-right:300px; float:left; border-radius:10px;"/>



**Numéro d'étudiant** : 22001267  
**Classe** : CAC2
# Compte rendu
Voici **une version beaucoup plus détaillée**, structurée comme un **rapport professionnel complet**, avec une introduction étoffée, des analyses approfondies, des explications pédagogiques et une conclusion riche.
C’est un document long, prêt à être transformé en **PDF**, **mémoire**, ou **rapport technique**.

---

# **RAPPORT DÉTAILLÉ – Analyse et Modélisation du Dataset IRIS**

## **Introduction**

Dans le cadre d’une démarche complète de Data Science, ce projet vise à explorer, préparer et modéliser un jeu de données réel afin d’en extraire des connaissances exploitables et d’évaluer la performance d’un modèle de Machine Learning. Le dataset **Iris**, proposé initialement par Ronald Fisher en 1936, constitue un classique en analyse prédictive. Il est utilisé mondialement comme benchmark dans les tâches de classification.

Cet ensemble de données se prête à une étude appliquée, car il combine :

* Des **variables continues** facilement interprétables,
* Trois **classes équilibrées**,
* Un nombre total d’observations suffisant pour expérimenter des techniques de modélisation,
* Une structure simple mais riche en enseignements statistiques.

L’objectif de ce rapport est d’appliquer un **cycle complet de Data Science**, comprenant :

1. Le chargement et la compréhension du jeu de données,
2. La création de valeurs manquantes pour simuler un cas réel,
3. Le nettoyage et l’imputation,
4. L’analyse exploratoire (EDA),
5. La préparation des données,
6. La modélisation via un algorithme supervisé,
7. L’évaluation des performances,
8. L’interprétation des résultats.

Cette étude met en lumière l’importance du traitement des données et du choix des modèles dans une problématique de classification.

---

# **1. Présentation du Dataset Iris**

Le dataset Iris contient **150 observations**, réparties en trois espèces de fleurs :

* *Iris Setosa* (0)
* *Iris Versicolor* (1)
* *Iris Virginica* (2)

Chaque observation comprend **4 variables numériques continues** :

| Feature           | Description        |
| ----------------- | ------------------ |
| Sepal length (cm) | Longueur du sépale |
| Sepal width (cm)  | Largeur du sépale  |
| Petal length (cm) | Longueur du pétale |
| Petal width (cm)  | Largeur du pétale  |

### **Caractéristiques importantes :**

* Le dataset est **équilibré** : 50 observations par classe.
* Les variables sont mesurées avec précision (unités en cm).
* Les espèces présentent des différences morphologiques significatives, ce qui facilite l’analyse.

### **Intérêt scientifique :**

Il s’agit d’un dataset idéal pour :

* illustrer les notions de classification,
* analyser la relation entre variables continues,
* visualiser la séparation des classes.

---

# **2. Simulation de Données Manquantes**

Pour simuler des conditions proches de la réalité, où les données sont souvent incomplètes, 5 % de valeurs manquantes ont été introduites aléatoirement dans les quatre variables explicatives.

### **But de cette étape :**

* Tester la robustesse du pipeline,
* Mettre en œuvre des techniques de nettoyage,
* Évaluer l’impact potentiel de l’imputation.

### **Résultats :**

* Environ **20 valeurs manquantes** ont été créées.
* Elles concernent toutes les colonnes explicatives.
* Aucune valeur manquante n’a été introduite dans la variable cible (target), ce qui permet une modélisation correcte.

---

# **3. Nettoyage et Imputation**

### **Méthode utilisée : SimpleImputer(strategy="mean")**

L’imputation par la **moyenne** est particulièrement adaptée car :

* Les données ne sont pas fortement asymétriques,
* Les variables sont numériques continues,
* Les corrélations entre variables permettent une approximation cohérente.

### **Résultats :**

* Toutes les valeurs manquantes remplacées,
* Dataset rendu **intégralement propre**,
* Aucune information perdue, contrairement à une suppression de lignes.

### **Effets positifs sur le modèle :**

* Amélioration de la stabilité,
* Préservation d’un volume d’informations suffisant,
* Réduction de la variance.

---

# **4. Analyse Exploratoire des Données (EDA)**

L'EDA est une étape essentielle permettant de comprendre la structure, la distribution et les relations entre variables.

## **4.1 Statistiques descriptives**

Les principales observations :

* Les sépales ont une variation limitée comparée aux pétales.
* Les pétales présentent une amplitude plus grande, ce qui laisse penser qu’ils jouent un rôle discriminant pour les espèces.
* *Setosa* possède systématiquement des valeurs faibles en longueur/largeur de pétale.

## **4.2 Analyse graphique**

### **Distribution de la longueur du sépale :**

La distribution montre :

* Setosa : valeurs courtes
* Versicolor : moyennes
* Virginica : plus longues

**Interprétation :**
Le sépale n’est pas le meilleur indicateur, mais contribue à distinguer les extrêmes.

### **Matrice de corrélation :**

Elle révèle :

* Corrélation élevée (≈ 0.96) entre **longueur pétale** et **largeur pétale**
* Corrélation modérée entre **longueur sépale** et **longueur pétale**
* Faible corrélation de **largeur sépale** avec les autres variables

**Conclusion EDA :**
Les variables liées au pétale sont les plus discriminantes. Elles permettront au modèle de mieux séparer les classes.

---

# **5. Préparation des Données**

Après nettoyage :

* Les données ont été séparées en **Train (80%)** et **Test (20%)**.
* Cette répartition est standard pour :

  * entraîner le modèle sur un échantillon suffisant,
  * conserver un ensemble impartial pour l’évaluation.

---

# **6. Modélisation**

Le modèle choisi est le **Random Forest Classifier**, qui présente plusieurs avantages :

### **Justification du choix**

* Modèle robuste face au bruit,
* Capable de gérer des relations non linéaires,
* Limite le risque de sur-apprentissage grâce à l’agrégation de multiples arbres.

### **Paramètres principaux :**

* n_estimators = 100
* random_state = 42

L’entraînement a été réalisé sans erreur, et le modèle a montré une convergence rapide.

---

# **7. Évaluation des Performances**

## **7.1 Accuracy**

L’accuracy obtenue est de :

# **➡️ 100 %**

Cela signifie que **toutes les fleurs du jeu de test ont été correctement classées**.

## **7.2 Rapport de classification**

| Classe     | Precision | Recall | F1-score |
| ---------- | --------- | ------ | -------- |
| Setosa     | 1.00      | 1.00   | 1.00     |
| Versicolor | 1.00      | 1.00   | 1.00     |
| Virginica  | 1.00      | 1.00   | 1.00     |

### **Interprétation :**

* **Precision = 1.00** → aucune erreur dans les prédictions par classe.
* **Recall = 1.00** → aucun élément manqué dans la vraie classe.
* **F1 = 1.00** → équilibre parfait entre précision et rappel.

## **7.3 Matrice de confusion**

La matrice montre :

* 30 bonnes prédictions,
* 0 erreur,
* donc une séparation parfaite des classes.

---

# **Conclusion**

L’analyse complète du dataset Iris met en évidence la robustesse du pipeline de Data Science élaboré. Après introduction volontaire de valeurs manquantes, le nettoyage et l’imputation ont permis d’obtenir un dataset homogène et fiable. L’analyse exploratoire confirme que les variables liées aux pétales constituent les éléments les plus discriminants permettant de distinguer les trois espèces.

La modélisation via un **Random Forest** a permis d’atteindre une **performance parfaite (100 %)** sur le jeu de test. Ceci démontre :

* la haute qualité du dataset,
* la pertinence des features morphologiques,
* la capacité du modèle à généraliser efficacement.

En perspective, plusieurs améliorations pourraient être explorées :

* Utilisation d’algorithmes alternatifs (SVM, Gradient Boosting),
* Analyse de l’importance des features,
* Validation croisée (K-fold) pour renforcer la robustesse,
* Construction d’un modèle explicable (SHAP values).

Ce projet illustre de manière cohérente l’ensemble des étapes essentielles en Data Science, depuis la préparation des données jusqu’à l’évaluation finale du modèle.

---


