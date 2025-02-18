# challenge_transilien
Repo créé dans le cadre du challenge ENS Transilien SNCF

Je participe seul à ce challenge. 
Mon objectif est de pratiquer afin d'améliorer mes compétences en datascience.


# Contexte
Transilien SNCF Voyageurs est l’opérateur des trains de banlieue en Île-de-France. Nous faisons circuler plus de 6 200 trains permettant à 3,4 millions de voyageurs de se déplacer. Chaque jour, nos trains desservent des milliers d’arrêt, pour faire en sorte que votre voyage se passe au mieux nous donnons un temps d’attente estimé, en minutes à droite sur la Figure 1. Nous souhaitons explorer la possibilité d’améliorer la qualité des prévisions de temps d’attente.

# Description des données
## Structure des données
• Un jeu de données x_train.csv avec 667 265 lignes (i.e. 667 265 arrêts k, s, d) et 10 colonnes
• Un jeu de données x_test.csv avec 20 658 lignes (i.e. 20 658 arrêts k, s, d) et 12 colonnes
• Un jeu de données y_train.csv avec 667 265 lignes et une colonne, donnant la variable à prédire pour le jeu d’entraînement
• Un jeu de données y_sample.csv avec 20 658 lignes et une colonne dont les valeurs sont aléatoires entre [-10, 10]. Il s’agit d’un exemple de soumission que vous pouvez prendre en exemple pour préparer votre soumission

## Origine des données
Ces données sont issues d’applications métiers permettant d’obtenir les heures théoriques et observées d’arrivées et de départ des trains en gare.
Les données anonymisées sont structurées de la manière suivante, une observation est un arrêt de train (cle_train) à une gare (cle_gare) donnée pour un jour donné (date). La variable p0q0 est la différence entre le temps d’attente théorique et réalisé. S’il est négatif, cela signifie que le temps d’attente est plus long que prévu sinon cela signifie qu’il est plus court. La différence de temps d’attente est entière car par soucis de simplicité pour nos voyag.eurs.euses nous n’affichons que des minutes sur nos écrans.
Nous vous demandons de prédire la différence de temps d’attente à deux gares en temps réel. Nous introduisons p et q pour définir le passé : p définit les valeurs passées aux arrêts précédents pour le même train, q définit les valeurs passées pour le précédent train à la même gare.
La différence de temps d’attente observé est p0q0 qui est la différence de temps d’attente, noté Y(k,s,d), pour un arrêt, soit un train k à la gare s le jour d.
Les colonnes, i.e., les variables explicatives, correspondent à 4 variables contextuelles et 6 valeurs passées :

## Variables contextuelles :
train (k) : numéro de train (unique par jour)
gare (s) : est l’identifiant de la gare
date (d) : YYYY-MM-DD est la date du jour où le train roule
arret : numéro de l’arrêt
Variables passées :
p2q0 : différence de temps d’attente du second train précèdent k-2 à la gare s
p3q0 : différence de temps d’attente du troisième train précèdent k-3 à la gare s
p4q0 : différence de temps d’attente du quatrième train précèdent k-4 à la gare s
p0q2 : différence de temps d’attente du même train k à la seconde gare précédente s-2
p0q3 : différence de temps d’attente du même train k à la troisième gare précédente s-3
p0q4 : différence de temps d’attente du même train k à la quatrième gare précédente s-4
Pour plus de détails sur la structure des données, je vous invite à consulter notre article de référence : One-Station-Ahead Forecasting of Dwell Time, Arrival Delay and Passenger Flows on Trains Equipped with Automatic Passenger Counting (APC) Device.

## Description du benchmark
Benchmark :
Le modèle de référence utilisé dans ce challenge est un modèle de forêt aléatoire classique.

## Métrique :
La métrique utilisée est une MAE (Mean Absolute Error) classique.
