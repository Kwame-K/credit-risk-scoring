# Scorecard logistique WoE — V1

## Objectif
Scorecard interprétable de prédiction du défaut, servant de benchmark
à comparer avec le futur modèle XGBoost.

## Données et découpage
- Variables initiales : 9
- Variables sélectionnées : 6
- Séparation temporelle : train, validation, test
- Taux de défaut test : 14.89%

## Performance sur test
- AUC ROC : 0.6300
- Gini : 0.2600
- KS : 0.1885
- Brier score : 0.1238
- AUC Precision-Recall : 0.2126

## Calibration
- Version retenue : Initiale
- Brier avant calibration : 0.1238
- Brier après calibration : 0.1239

## Stabilité
- PSI score train vs test : 0.0131
- Variable avec PSI maximal : purpose
- PSI maximal par variable : 0.0698

## Scorecard
- Score de référence : 600
- Odds de référence non-défaut / défaut : 50:1
- PDO : 20
- Contrôle de reconstitution : écart maximal = 0.0000000000

## Comparaison XGBoost
Le modèle XGBoost devra utiliser exactement les mêmes partitions
temporelles et être comparé sur AUC, AUC-PR, KS, Brier et PSI.
