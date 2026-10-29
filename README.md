# Projet TBD8 2025-2026 — Analyse de données Taxi avec PySpark

Projet réalisé dans le cadre du cours de Technologies Big Data (TBD8).

#Note a l'utilisateur 
Rentrer la commande cat Taxi_parts/Taxi.csv.part-* > Taxi.csv avant utilisation 

## Description

Ce projet a pour objectif de :

- nettoyer un jeu de données de trajets de taxi,
- vérifier la cohérence et la qualité des données,
- transformer les données avec PySpark,
- stocker les résultats au format Parquet partitionné,
- préparer les données pour des analyses Big Data.

Le dataset contient notamment :

- les timestamps des trajets,
- les distances,
- les montants payés,
- les coordonnées GPS,
- les zones de départ et d’arrivée.

## Structure du projet

```text
projet-tbd8-2026-gbaguidi-lauture/
├── notebook_version_1.ipynb
├── README.md
├── Taxi.csv
├── taxi_parquet/
└── .gitignore
```

## Étapes du pipeline

### 1. Chargement des données

Lecture du fichier CSV brut avec Spark :

```python
spark.read.option("header", "true").csv(...)
```

### 2. Nettoyage des données

Le pipeline effectue notamment :

* nettoyage des noms de colonnes,
* conversion des colonnes numériques,
* parsing des dates américaines,
* suppression des doublons,
* suppression des valeurs nulles critiques,
* suppression des lignes incohérentes.

Exemples de vérifications :

* distance > 0,
* durée > 0,
* timestamps cohérents,
* coordonnées GPS valides,
* vitesse moyenne réaliste,
* cohérence entre `Trip_Total` et `Fare + Tips + Tolls + Extras`

### 3. Vérification de qualité

Des indicateurs sont calculés :

* vitesse moyenne minimale / maximale,
* prix par mile,
* différence entre durée calculée et durée déclarée,
* différence tarifaire.

### 4. Stockage en Parquet

Les données nettoyées sont sauvegardées en Parquet avec partitionnement par mois :

```python
.partitionBy("Trip_month")
```

Cela permet :

* des lectures plus rapides,
* moins de données scannées,
* de meilleures performances Spark.

## Lancement du projet : Exécuter le notebook

Ouvrir le notebook dans Jupyter ou Polynote puis exécuter les cellules dans l’ordre.

## Auteurs

* Nerval GBAGUIDI
* Marie LAUTURE
