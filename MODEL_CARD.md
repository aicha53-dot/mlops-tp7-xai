
# Model Card - fraude (version servie par l'alias production)

## Modèle
Nom et version : fraude, version 1, alias production.

Famille : RandomForestClassifier, 500 arbres, profondeur maximale 16.

Run d'origine MLflow : 063e5b4c24494f04833ddf406427960d

## Objectif et usage prévu
Détecter les transactions bancaires potentiellement frauduleuses afin d'aider les équipes de contrôle à identifier les opérations suspectes.

## Usages exclus
Ne pas utiliser pour bloquer définitivement un compte ou accuser un client de fraude sans vérification humaine.

## Données
Fichier : data/transactions.csv

5 000 transactions synthétiques, dont 568 fraudes (11,36 %).

Empreinte MD5 : cf9f6f86c141e7df32c61715c493483f

Variables : montant, anciennete, freq_24h et nuit.

## Performances
Évaluation sur 1 250 transactions de test, dont 134 fraudes.

- F1-score : 0.8669
- Précision : 0.8837
- Rappel : 0.8507
- ROC-AUC : 0.9872
- Matrice de confusion : [[1101, 15], [20, 114]]

## Méthodes d'explicabilité
Globales : importance par permutation et SHAP TreeExplainer.

Locales : SHAP et LIME.

Le montant est la variable la plus importante globalement.

Pour Mme Benali, SHAP identifie principalement la nuit (+0.3697) et le montant (+0.3665).

Probabilité de fraude estimée : 92,4 %.

## Comparaison avec un modèle interprétable
Forêt aléatoire : F1 = 0.8669, 114 fraudes détectées.

Régression logistique avec log10(montant) : F1 = 0.8593, 113 fraudes détectées.

Arbre de profondeur 3 : F1 = 0.5737, 72 fraudes détectées.

La régression logistique offre un compromis intéressant entre performance et interprétabilité.

## Limites et risques connus
Les données sont synthétiques : les performances ne sont pas validées sur des transactions bancaires réelles.

Le modèle génère 15 fausses alertes et manque 20 fraudes sur le jeu de test.

Les contributions SHAP ne prouvent pas une causalité. Les explications LIME varient selon la graine aléatoire.

## Recommandations d'utilisation et de surveillance
Prévoir une vérification humaine des alertes.

Surveiller le F1-score, le rappel, les fausses alertes et les évolutions des données.

Réévaluer le modèle avant tout déploiement bancaire réel.

## Traçabilité
Expérience MLflow : tp7-explicabilite

Run des explications : 9fe6f31ecfa446d08c85b4675690776f

Version du modèle : fraude v1

Date : 10/11/2026

Auteurs : Aicha EL Bekali - Malak Achari

Prochaine revue : 10/12/2026