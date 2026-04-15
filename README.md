# Min Max - Fanorona Telo

Un jeu de stratégie "Fanorona Telo" implémenté en Python avec interface graphique et algorithme minimax pour l'IA.

## Description

**Fanorona Telo** est un jeu de plateau traditionnel malgache pour deux joueurs. Ce projet propose une implémentation complète avec :

- Interface graphique interactive développée avec Tkinter
- Système d'IA utilisant l'algorithme Minimax
- Gestion d'état du jeu et arbre de recherche
- Support pour deux joueurs : Humain vs IA ou IA vs IA
- Points noirs comme obstacles stratégiques pour enrichir le gameplay

## Structure du Projet

```
min_max/
├── display/              # Interface graphique
│   ├── Fenetre.py       # Fenêtre principale
│   ├── Table.py         # Plateau de jeu
│   ├── Main.py          # Point d'entrée de l'application
│   └── Info.py          # Affichage des informations
├── fonction/            # Logique du jeu
│   ├── Fonction.py      # Algorithme Minimax et utilitaires
│   ├── Data.py          # Données partagées du jeu
│   ├── Ecouteur.py      # Gestion des événements
│   └── Mouse.py         # Gestion de la souris
├── form/                # Structures géométriques
│   ├── Point.py         # Classe Point
│   ├── Node.py          # Nœud d'arbre de jeu
│   ├── Graphe.py        # Graphe de jeu
│   └── Rectangle.py     # Classe Rectangle
├── objets/              # Objets du jeu
│   ├── Player.py        # Classe Joueur
│   └── Box.py           # Classe Boîte
├── main.py              # Script de test
└── requirements.txt     # Dépendances
```

## Installation

### Prérequis

- Python 3.8 ou supérieur
- pip (gestionnaire de paquets Python)

### Initialiser l'environnement virtuel

#### Sur Windows (PowerShell ou CMD)

```powershell
# Créer l'environnement virtuel
python -m venv venv

# Activer l'environnement virtuel
.\venv\Scripts\Activate.ps1

# Installer les dépendances
pip install -r requirements.txt
```

#### Sur Linux/macOS

```bash
# Créer l'environnement virtuel
python3 -m venv venv

# Activer l'environnement virtuel
source venv/bin/activate

# Installer les dépendances
pip install -r requirements.txt
```

### Dépendances principales

- **numpy** (2.4.4) - Manipulation de tableaux numériques
- **Shapely** (2.1.2) - Géométrie computationnelle
- **pyodbc** (5.3.0) - Accès aux bases de données ODBC

## Utilisation

Une fois l'environnement virtuel activé, lancez l'application :

```bash
python -m display.Main
```

L'interface graphique Tkinter s'ouvrira avec un plateau de jeu 3x3.

## Galerie

### Captures d'écran

#### Interface du Jeu
![Interface principale du jeu Fanorona Telo](./docs/image1.jpg)

#### Plateau de Jeu
![Plateau de jeu 3x3 avec les pièces](./docs/image2.jpg)


#### En Action
![Exemple d'une partie en cours](./docs/image3.jpg)

## Fonctionnalités Principales

### Algorithme Minimax

L'algorithme Minimax implémenté permet à l'IA de prendre les meilleures décisions :

- Exploration récursive de l'arbre de jeu
- Profondeur de recherche configurable via `Data.profondeur`
- Évaluation des positions en fonction des scores
- Optimisations pour limiter la complexité computationnelle

### Gestion Géométrique

Le projet intègre une gestion sophistiquée des coordonnées et des distances :

- Classe Point pour les coordonnées du jeu
- Calcul des distances euclidiennes entre points
- Détection des points proches (proximité)
- Vérification de la colinéarité pour les mouvements

### Interface Graphique

L'interface développée en Tkinter offre une expérience intuitive :

- Plateau de jeu interactif et réactif
- Affichage en temps réel du score et des informations
- Gestion des événements souris pour les coups du joueur
- Visualisation claire du jeu et des mouvements

## Modules Clés

### fonction/Fonction.py

Contient la logique centrale du jeu :

- `min_max()` - Algorithme Minimax principal pour les décisions de l'IA
- `distance()` - Calcul de distance euclidienne entre deux points
- `sont_colineaires()` - Vérification de la colinéarité de points
- `estProche()` - Détection de proximité entre deux points

### display/Main.py

Point d'entrée principal de l'application :

- Configuration des joueurs
- Initialisation de l'interface graphique
- Mise en place du plateau de jeu

### form/Point.py et form/Node.py

Structures fondamentales pour le jeu :

- Point : Représentation des positions sur le plateau
- Node : Nœuds de l'arbre de recherche Minimax

### objets/Player.py

Gestion des joueurs et de leurs scores

## Comment Jouer

### Mode Humain vs IA

1. Lancez l'application en suivant les instructions d'utilisation
2. Cliquez sur les points du plateau pour effectuer vos coups
3. L'IA répondra automatiquement en utilisant l'algorithme Minimax
4. Observez votre score et celui de votre adversaire dans le panneau d'information

### Mode IA vs IA

Pour observer deux IA s'affronter, modifiez `display/Main.py` pour que les deux joueurs jouent automatiquement :

- Les deux IA utiliseront l'algorithme Minimax pour leurs décisions
- Idéal pour tester et analyser différentes stratégies
- Permet d'observer l'évolution du jeu et les décisions de l'algorithme

## Points Noirs - Obstacles Stratégiques

Les points noirs sont des éléments clés du plateau qui modifient la dynamique du jeu :

- **Bloquent les mouvements** - Impossibles à franchir pour les pièces
- **Divisent le plateau** - Créent des zones de jeu distinctes
- **Augmentent la complexité** - Réduisent l'espace de recherche disponible
- **Enrichissent la stratégie** - Forcent les joueurs à adapter leurs tactiques

### Configuration des Points Noirs

Modifiez la liste `Data.point_noires` dans `display/Main.py` pour ajouter ou retirer des obstacles :

```python
Data.point_noires = [
    Point(415, 415),  # Point noir au centre
    Point(135, 135),  # Point noir en haut à gauche
]

for point_noire in Data.point_noires:
    Data.table.drawPoint(point_noire, "black")
```

Par exemple, un point noir au centre du plateau 3x3 le divise en 4 zones distinctes, augmentant considérablement la profondeur stratégique du jeu.

## Configuration

Les paramètres du jeu peuvent être modifiés dans `fonction/Data.py` :

- `Data.profondeur` - Profondeur de l'arbre Minimax (augmenter pour une IA plus forte mais plus lente)
- `Data.players` - Liste des joueurs en jeu
- `Data.point_noires` - Points qui bloquent les mouvements sur le plateau
- `Data.fenetre` - Référence à la fenêtre principale
- `Data.table` - Instance du plateau de jeu
- `Data.info` - Panneau d'affichage des informations

## Notes de Développement

- Les coordonnées utilisent un système (x, y) standard
- L'algorithme Minimax explore tous les coups possibles jusqu'à une profondeur donnée
- L'IA évalue les positions en fonction des scores des joueurs
- Distance minimale pour considérer deux points comme proches : 396 unités

## Fichiers Supplémentaires

- **requirements.txt** - Liste des dépendances Python
- **bck.txt** - Fichier de sauvegarde
- **output.txt** - Résultats et logs de sortie
- **optimisez.txt** - Notes d'optimisation et améliorations

## Auteur

Projet développé par Tsialone

## License

À spécifier

## Notes de Développement

- Le projet utilise des points avec des coordonnées (x, y)
- L'algorithme Minimax explore tous les coups possibles jusqu'à une profondeur donnée
- L'IA évalue les positions en fonction des scores des joueurs
- Distance minimale pour considérer deux points comme proches : 396 unités

## Fichiers de Configuration

- **requirements.txt** : Dépendances Python
- **output.txt** : Résultats/logs de sortie

## Auteur

Projet développé par **Tsialone**

## License

Opensource

---

**Bon jeu ! 🎮**
