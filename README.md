## Résumé du projet – Prédiction de la pluie (RainTomorrow)

### Objectif
Prédire si **la pluie surviendra le lendemain** (`RainTomorrow`) à partir de données météorologiques, en comparant plusieurs modèles de machine learning et en étudiant l’impact de la **réduction de dimension (PCA)**.

---

### Données
- **Source** : `Data_Weather.csv`
- **Taille** : 145 460 observations, 22 variables explicatives
- **Cible** : `RainTomorrow` (Oui / Non)
- **Déséquilibre de classes** :
  - No : ~78 %
  - Yes : ~22 %

---

### Analyse exploratoire (EDA)
- Aucune valeur manquante après inspection
- Analyse des distributions et corrélations
- Visualisation du déséquilibre de la variable cible

---

### Prétraitement des données
- Suppression des colonnes non informatives (`Date`, `Location`)
- Encodage de la variable cible (Yes = 1, No = 0)
- Séparation **Train / Test (80 % / 20 %)** avec stratification
- Pipeline appliqué uniquement sur le jeu d’entraînement :
  - Imputation des valeurs manquantes
  - Traitement des valeurs aberrantes (IQR)
  - Encodage One-Hot des variables catégorielles
  - Standardisation des variables numériques
  - Suppression des variables fortement corrélées
  - Rééquilibrage des classes avec **SMOTE**

---

### Réduction de dimension (PCA)
- Variables avant PCA : **60**
- PCA conservant **75 % de la variance**
- Nombre de composantes principales : **31**
- Réduction de dimension : **–48 %**

---

### Modèles entraînés
1. **Régression logistique**
2. **KNN (sans réduction de dimension)**
3. **KNN avec PCA**

Optimisation des hyperparamètres de KNN via **GridSearchCV**.

---

### Résultats (jeu de test)
La **régression logistique** obtient les meilleures performances globales, notamment en **ROC-AUC** et **F1-score**, tandis que le **KNN** est plus sensible à la dimensionnalité des données.

---

### Interprétabilité
L’analyse des coefficients de la régression logistique montre que :
- **Humidity3pm** est la variable la plus déterminante
- La vitesse et la direction du vent jouent un rôle majeur dans la prédiction de la pluie

---

### Visualisations & analyses complètes
Pour consulter **tous les graphiques, comparaisons détaillées, matrices de confusion, courbes ROC, validation croisée et métriques complètes** pour les modèles **KNN** et **régression logistique** (classification météorologique), voir le notebook complet :

**Notebook GitHub**  
https://github.com/Enzo-JZN/Model-ML/blob/main/notebooks/main_notebook.ipynb

---

### Conclusion
- La **régression logistique** offre le meilleur compromis entre performance et interprétabilité
- Le **PCA** permet de réduire la dimension mais impacte légèrement les performances de KNN
- Le rééquilibrage **SMOTE** améliore la détection des jours pluvieux

**Modèle recommandé : Régression logistique sans PCA**
