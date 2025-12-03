# HAMINE Hajar

<img src="" style="height:300px;margin-right:300px; float:left; border-radius:10px;"/>


**Numéro d'étudiant** : 22001267  
**Classe** : CAC2
# Compte rendu
## Analyse Prédictive de Régression sur les Prix de Voitures

*Date :* 03 Décembre 2025

---

## Table des Matières

1.  [Introduction et Contexte](#1-introduction-et-contexte)
2.  [Analyse Exploratoire des Données (Data Analysis)](#2-analyse-exploratoire-des-données-data-analysis)
    * [Chargement et Structure du Dataset](#21-chargement-et-structure-du-dataset)
    * [Variable Cible et Variables Explicatives](#22-variable-cible-et-variables-explicatives)
    * [Analyse Statistique et Visuelle](#23-analyse-statistique-et-visuelle)
3.  [Méthodologie de Régression](#3-méthodologie-de-régression)
    * [Préparation des Données](#31-préparation-des-données)
    * [Séparation des Données (Train / Test)](#32-séparation-des-données-train--test)
    * [Modèles de Régression Testés](#33-modèles-de-régression-testés)
4.  [Résultats et Analyse Comparative](#4-résultats-et-analyse-comparative)
    * [Régression Linéaire](#41-régression-linéaire)
    * [Régression par Arbre de Décision](#42-régression-par-arbre-de-décision)
    * [Régression par Forêt Aléatoire](#43-régression-par-forêt-aléatoire)
5.  [Conclusion](#5-conclusion)

---

## 1. Introduction et Contexte

Ce rapport présente une analyse prédictive de régression sur un jeu de données réel concernant les caractéristiques de voitures et leur prix de vente, importé depuis Kaggle :  
“Car Features and Selling Price Analysis Dataset”.

En suivant le cycle de vie des données, nous avons mené une exploration (EDA), un prétraitement et une modélisation prédictive.

L’objectif est de construire des modèles de régression capables de prédire le **prix de vente** (*selling_price*) d’une voiture à partir de ses caractéristiques (année, kilométrage, type de carburant, boîte de vitesses, etc.) et de comparer les performances de plusieurs algorithmes de régression.

---

## 2. Analyse Exploratoire des Données (Data Analysis)

### 2.1 Chargement et Structure du Dataset

Le jeu de données Kaggle contient les caractéristiques de voitures d’occasion et leur prix de vente.

- Nombre d’échantillons (\(N\)) : affiché par `df.shape[0]`.
- Nombre de variables (\(d\)) : affiché par `df.shape[1]`.

Variables typiques présentes dans le dataset (peuvent varier selon la version) :

- car_name : nom / modèle du véhicule
- year : année de mise en circulation
- selling_price : prix de vente (variable cible)
- km_driven : kilométrage
- fuel : type de carburant (Petrol, Diesel, CNG, etc.)
- seller_type : type de vendeur (Individual, Dealer, etc.)
- transmission : type de boîte (Manual, Automatic)
- owner : nombre de propriétaires précédents

