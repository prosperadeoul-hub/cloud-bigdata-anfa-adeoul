# Rendu — Séance 10

**Nom et prénom :** <ADEOUL Koffi Prosper>

**Identifiant GitHub :** <prosperadeoul-hub>

**Date de soumission :** <14/07/2005>

## Résumé de la séance

Lors de cette séance, j'ai déployé un serveur MLflow pour tracer l'entraînement de nos modèles de prédiction d'affluence. Après avoir généré un jeu de données synthétique, j'ai entraîné trois variantes d'un modèle RandomForest avec différents hyperparamètres, puis je les ai comparées directement dans l'interface graphique de MLflow. Pour finir, j'ai enregistré la version la plus performante dans le Model Registry en la passant au statut Production, avant de formaliser l'ensemble de notre gouvernance de données à travers une fiche de conformité RGPD/Loi togolaise.

## Étapes principales

1. Déploiement d'un serveur MLflow Tracking (SQLite + stockage local).
2. Génération d'un jeu de données d'affluence Anfa et entraînement de 3 variantes
   d'un modèle RandomForest, chacune tracée avec MLflow.
3. Comparaison des runs dans l'UI et identification du meilleur candidat.
4. Enregistrement du modèle dans le Model Registry, transition en statut Production.
5. Rédaction d'une fiche de conformité pour un scénario d'application mobile Anfa.

## Captures d'écran

### Tableau des 3 runs comparés
![Runs MLflow](captures/mlflow-runs.png)

### Modèle enregistré en statut Production
![Registry Production](captures/mlflow-registry-production.png)

## Réflexion personnelle

Le Model Registry résout le désordre de Kossi en centralisant, traçant et versionnant rigoureusement chaque version de modèle au sein d'un cycle de vie clair (Staging, Production), évitant ainsi les notebooks dispersés. Tout comme Terraform (séance 4) automatise et standardise le déploiement d'une infrastructure via du code déclaratif, MLflow standardise et automatise la gestion des modèles en les transformant en artefacts auditables. Dans les deux cas, on élimine l'arbitraire humain pour garantir la reproductibilité et la traçabilité de bout en

## Difficultés rencontrées

<Aucune>
