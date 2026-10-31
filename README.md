# Quixo 🎲

Jeu de stratégie **Quixo** en ligne de commande, joué contre un serveur distant via une API REST. Le programme peut être contrôlé par un humain ou jouer seul grâce à une **IA** qui cherche les coups gagnants et bloque l'adversaire.

**Règle du jeu** : sur un plateau 5×5, chaque joueur retire un cube de la bordure et le réinsère à l'extrémité d'une ligne ou d'une colonne en poussant les autres. Le premier à aligner 5 symboles gagne.

## Technologies

| Domaine | Outils |
|---|---|
| Langage | Python 3 |
| Réseau | `requests` (API REST, authentification HTTP Basic) |
| Ligne de commande | `argparse` |
| Qualité | Pylint, tests unitaires fournis |
| Versionnement | Git |

## Fonctionnalités

- Création d'une partie, envoi des coups et récupération de l'état via l'API du serveur.
- Affichage du plateau en ASCII dans le terminal.
- Validation des entrées et gestion d'erreurs personnalisée (`QuixoError`, codes HTTP 401 / 406).
- **Mode autonome** (`-a`) : l'IA joue toute la partie seule.

## Aperçu

```text
$ python3 main.py mon_idul
Légende:
   X=mon_idul
   O=robot
   -------------------
1 | X |   |   | O |   |
  |---|---|---|---|---|
2 |   | X |   |   |   |
  |---|---|---|---|---|
3 | O |   | X |   |   |
  |---|---|---|---|---|
4 |   |   |   |   | O |
  |---|---|---|---|---|
5 |   |   |   |   |   |
--|---|---|---|---|---|
  | 1   2   3   4   5 |

Donnez la position d'origine du cube (x, y) : 5,5
Quelle direction voulez-vous insérer? ('haut', 'bas', 'gauche', 'droite') : haut
```

<!-- IMAGE (optionnelle) : capture du terminal pendant une partie en mode autonome (python3 main.py mon_idul -a 1) -->

## Stratégie de l'IA

À chaque tour, l'IA :
1. liste tous les coups légaux depuis la bordure du plateau ;
2. joue un **coup gagnant** si une ligne, colonne ou diagonale contient déjà 4 de ses cubes ;
3. sinon, joue un **coup bloquant** si l'adversaire est sur le point de gagner ;
4. sinon, choisit un coup légal au hasard.

## Structure

| Fichier | Rôle |
|---|---|
| `main.py` | Boucle de jeu (mode manuel ou autonome) |
| `api.py` | Communication avec le serveur de jeu |
| `quixo.py` | Classe `Quixo` et interpréteur de commande |
| `plateau.py` | Classe `Plateau` : représentation et insertion des cubes |
| `quixo_ia.py` | Classe `QuixoIA` (hérite de `Quixo`) |
| `quixo_error.py` | Exception personnalisée |

## Mes tâches

- Implémentation complète du client : appels API, boucle de jeu, affichage.
- Conception orientée objet (`Plateau`, `Quixo`, `QuixoIA`) avec héritage et méthodes spéciales (`__str__`, `__getitem__`, `__setitem__`).
- Développement de l'IA (détection des coups gagnants et bloquants).
- Validation des entrées et gestion des erreurs.

## Ce que j'ai appris

- Consommer une **API REST** depuis Python et traiter les codes d'erreur HTTP.
- Structurer un programme en **classes** et utiliser l'héritage pour étendre un comportement (joueur humain → IA).
- Utiliser les **méthodes spéciales** Python pour rendre un objet indexable comme une liste.
- Construire une interface **en ligne de commande** avec `argparse`.
- Concevoir une IA simple basée sur des règles et analyser un plateau (lignes, colonnes, diagonales).
- Écrire du code propre et documenté (docstrings, Pylint) et versionner avec Git.

## Code source

Le code source est hébergé dans un dépôt privé (projet universitaire, Université Laval). Il est disponible sur demande.
