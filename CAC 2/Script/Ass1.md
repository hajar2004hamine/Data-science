<img src="image.jpg" style="height:464px;margin-right:432px"/>
#HAJAR HAMINE
# apogée 22001267
# 🩺 Analyse descriptive de la base de données Heart Disease

## 1. Présentation générale du jeu de données
Le jeu **Heart Disease** contient des informations médicales sur des patients, avec l’objectif de **déterminer la présence ou non d’une maladie cardiaque**.  
Chaque ligne correspond à un patient, et chaque colonne à une caractéristique médicale.

### Les principales variables (colonnes)
| N° | Variable | Signification |
|----|-----------|----------------|
| 1 | **age** | Âge du patient (en années) |
| 2 | **sex** | Sexe (1 = homme, 0 = femme) |
| 3 | **cp** | Type de douleur thoracique (0–3, de l’absence à la douleur typique) |
| 4 | **trestbps** | Tension artérielle au repos (mm Hg) |
| 5 | **chol** | Taux de cholestérol sérique (mg/dl) |
| 6 | **fbs** | Glycémie à jeun > 120 mg/dl (1 = oui, 0 = non) |
| 7 | **restecg** | Résultat de l’électrocardiogramme au repos |
| 8 | **thalach** | Fréquence cardiaque maximale atteinte |
| 9 | **exang** | Angine de poitrine induite par l’effort (1 = oui, 0 = non) |
| 10 | **oldpeak** | Dépression du segment ST induite par l’effort |
| 11 | **slope** | Pente du segment ST pendant l’effort |
| 12 | **ca** | Nombre de vaisseaux principaux colorés par fluoroscopie |
| 13 | **thal** | Type de thalassémie |
| 14 | **target** | Présence de maladie cardiaque (0 = non, 1 = oui) |

---

## 2. Analyse statistique descriptive

### Âge
- Moyenne ≈ **54 ans**  
- Minimum ≈ **29**, maximum ≈ **77**  
➡️ La majorité des patients sont d’âge moyen ou plus âgés, ce qui correspond bien à la population à risque.

### Sexe
- Environ **70 % d’hommes** et **30 % de femmes**.  
➡️ Les maladies cardiaques sont plus fréquentes chez les hommes dans cet échantillon.

### Tension artérielle (trestbps)
- Moyenne ≈ **131 mmHg**, maximum ≈ **200 mmHg**.  
➡️ Beaucoup de patients présentent une **hypertension** (supérieure à 120 mmHg).

### Cholestérol (chol)
- Moyenne ≈ **246 mg/dl**, certains dépassent **500 mg/dl**.  
➡️ Ces valeurs indiquent souvent une **hypercholestérolémie**, facteur de risque important.

### Fréquence cardiaque max (thalach)
- Moyenne ≈ **150 battements/minute**, max ≈ **200**.  
➡️ Les patients en bonne santé atteignent souvent des valeurs plus élevées.

### Dépression ST (oldpeak)
- Moyenne ≈ **1.0**, max ≈ **6.2**.  
➡️ Des valeurs élevées traduisent souvent un **stress cardiaque important** pendant l’effort.

### Nombre de vaisseaux colorés (ca)
- La plupart ont **0 ou 1 vaisseau obstrué**, mais certains en ont jusqu’à **4**.  
➡️ Plus ce nombre est grand, plus le risque de maladie cardiaque est fort.

---

## 3. Relations importantes observées (corrélations)
- **Âge** est modérément corrélé à la **tension** et au **cholestérol**.  
- **Fréquence cardiaque max** est **inversement corrélée** à l’âge.  
- **oldpeak**, **ca** et **thal** sont fortement liés à la **maladie cardiaque (target)**.  
➡️ Ce sont donc des **indicateurs prédictifs puissants**.

---

## 4. Interprétation globale
L’analyse montre :  
- Le **profil typique du patient malade** : homme de plus de 50 ans, tension élevée, cholestérol élevé, anomalies à l’ECG.  
- Le **profil typique du patient sain** : femme ou homme jeune, tension et cholestérol normaux, fréquence cardiaque élevée, aucune anomalie à l’effort.

---

## 5. Recommandations analytiques
Pour aller plus loin :  
1. Nettoyer les données (remplacer les “?” par des valeurs moyennes).  
2. Créer un modèle de **prédiction du risque cardiaque** (ex : régression logistique).  
3. Visualiser la répartition du “target” (0 = sain / 1 = malade).  
4. Faire une **analyse discriminante** entre les groupes.
