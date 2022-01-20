# Spécifications
[[toc]]

## Principes généraux

### Jeu
* Il n'existe qu'une et une seule version du jeu.

* Ce jeu doit nécessairement être joué par au moins un joueur pour exister.

* Il n'est pas nécessaire qu'une première série de matches aie été jouée pour que le jeu existe (les joueurs doivent en effet pouvoir se préparer avant de jouer leur première partie : choisir un avatar, le mode de jeu, le nombre de joueurs, ...).

### Series
* Une série de matches comprend au moins un match.

* Le nombre de match au sein d'une série est impair.

* Une série est jouée
    * DUEL :        soit en mode duel (2 joueurs uniquement)
    * MULTIPLAYER : soit en mode multijoueurs (3+ joueurs)

* Une série est jouée
    * REALTIME :   soit en mode temps-réel.
    * TURN_BASED : soit en mode tour-par-tour.

* Un seul match peut être joué à la fois.

### Match
* Un match est identifié de manière unique.

* Tout match se déroule sur un plateau propre.

* Un match voit se rencontrer les avatars des joueurs.

* Un match peut être gagné de deux manières :
    * LAST_MAN_STANDING : un seul joueur est encore en vie.
    * FOUND_GRAAL : un joueur a trouvé le GRAAL.

* Un match peut être libre ou limité:
    * FREE : sans limite
    * TIMER : soit par chronomètre
    * TURN : soit par compte-tours

* Selon le type d'adversaire, un match peut ou ne peut pas être chronométré.
    * Contre un ordinateur : FREE est autorisé.
    * Contre un ou plusieurs joueurs humains : FREE est interdit.

* La limite d'un match s'exprime soit:
    * en temps restant.
    * en tours restants.

### Joueur
* Un joueur est soit un être humain, soit un ordinateur.

* Un ordinateur a trois niveaux de difficulté possibles
    * EASY
    * NORMAL
    * EXPERT
* Un joueur possède des skins (figurines)

* Il a au moins le skin par défaut.

* Un joueur possède au moins un avatar (personnage dans le jeu) et peut en avoir davantage.

* Un joueur participe à des séries pour jouer.

### Avatar
* Un avatar est possédé par un et un seul joueur.

* Un avatar possède un identifiant unique parmi les avatars d'un joueur.

* Un avatar porte 1 et 1 seul skin (qui peut être changé).

* Un avatar se trouve au maximum sur une et une seule tuile.

* L'avatar possède un inventaire.

### Skin
* Un skin est soit libre, soit payant (_premium_).

* Un skin est disponible mais pas forcément encore acquis par un des joueurs.

* Un skin peut être porté par n'importe quel avatar, pour autant que le joueur l'aie acheté préalablement.

* Il existe au moins un skin non-payant.


## Principes de jeu

### Inventory
* L'inventaire d'un avatar contient nécessairement
    * un stock de munitions/boissons de 0 à N
    * un stock de nourriture de 0 à N

* Lorsqu'un consommable est activé, sa quantité diminue de 1.

* Un consommable en quantité zéro ne peut pas être activé.

* L'inventaire contient l'équipement éventuel.

* L'inventaire de l'avatar est permanent (survit à la fin du match et de la série).

### Board
* Un monde est de dimension figée et carré.

* Un monde est composé de cases.

* Un monde contient zéro, un ou plusieurs zombies (un nombre qui varie au gré des décès des zombies sous les coups des avatars des joueurs).

### Tile
* Une case peut
    * être vide
    * contenir un avatar
    * contenir un zombie
    * contenir un objet
    * contenir un obstacle

* une case ne peut pas contenir à la fois un joueur et un zombie.

### Obstacle
* Un obstacle se trouve sur une case

* Un obstacle peut parfois être franchissable, parfois destructible.

* Un obstacle peut être détruit s'il s'agit
  * THORN : de ronces
  * BUSH :  d'un buisson
  * TRUNK : d'un tronc d'arbre
  * SKULL : d'une tête de mort

* Un obstacle peut être franchi par l'avatar s'il remplit les conditions nécessaires au franchissement

* Un obstacle peut être franchi si
    * c'est une zone de feu.
    * l'avatar possède la cape de mage.
    * c'est une zone d'eau et l'avatar possède un kit de plongée
    * c'est une zone glacée et l'avatar possède des bottes à crampons

* Si l'obstacle est une zone de feu et que l'avatar la franchit,
    * Soit l'avatar possède des bottes pare-feu,
    * Soit il perd un point de vie par tour.

* Un obstacle n'est ni franchissable ni destructible s'il s'agit
    * WALL : d'un mur
    * TREE : d'un arbre
    * ROCK : d'un menhir

* Un obstacle qui est détruit disparaît

### Item
* Il existe trois types d'objets:
    * GRAIL :      le Graal
    * CONSUMABLE : les consommables
    * EQUIPMENT :  l'équipement

* Il n'existe qu'un et un seul graal sur la carte.

* Les consommables sont de trois types:
    * FOOD : Nourriture
    * DRINK : Boisson
    * AMMO : Munitions

* Les consommables doivent être activés par le joueur.
    * La nourriture et les boissons augmente la vie de 1.
    * les munitions déclenchent un tir à distance.

* L'équipement est divisé en plusieurs types :
    * BOOSTER :   Boosteurs
    * CAPACITER : Capaciteurs
    * POINTER :   Pointeurs
    * BUFF :      Muscleurs

* Les boosteurs sont des augmentations permanentes des caractéristiques de l'avatar et sont de deux types :
    * ATTACK :  Boosteur d'attaque
    * DEFENSE : Boosteur de défense

* Les boosteurs sont activés à la collecte.

* Les muscleurs sont des pouvoirs temporaires accordés à l'avatar et sont de deux types :
    * ARMOR : rend l'avatar invincible.
    * CAPE : permet de passer à travers tous les obstacles (max 3 fois pour les infranchissables)

* Les muscleurs ont une durée qui dépend du mode de jeu:
    * TURN_BASED: la durée correspond à [1/10 des points de vie de l'avatar]-tours.
    * REALTIME:   la durée correspond à 1 minute.

* Les capaciteurs sont des augmentations permanentes des capacités de l'avatar et sont de trois types :
    * FIREBOOT: permet de franchir l'obstacle FIRE sans dommage.
    * ICEBOOT: permet de franchir l'obstacle ICE.
    * DIVEMASK: permet de franchir l'obstacle WATER.

* Les pointeurs sont des outils de guidage et sont de deux types :
    * MAP (permanent) : indique la direction à vol d'oiseau vers le GRAAL
    * RADAR (temporaire) : indique la direction à vol d'oiseau vers l'adversaire

* Les pointeurs sont activés à la collecte.

* Le pointeur RADAR est actif pendant _n_-tours.

* Si un radar est actif et qu'un nouveau radar est collecté, la valeur _n_ restante est doublée.

* Le pointeur MAP disparaît de l'inventaire à la fin du match.

* Un objet est automatiquement ramassé par le joueur qui passe dessus.

* Un objet ramassé disparaît du plateau et apparaît dans l'inventaire du joueur.

### Zombie
* Un zombie est présent sur une et une seule tuile.

* Un zombie a un ensemble de points de vie.

* Si cet ensemble de points de vie atteint zéro, le zombie meurt.

* Un zombie mort disparaît du plateau.

---

## Description des stratégies

### Stratégie
* Une stratégie est composée
    * de variables globales ;
    * de modules ;
    * d'objectifs ;
    * de règles.

* Tous les modules au sein d'une stratégie sont nommés différemments.
* Toutes les variables globales au sein d'une stratégie sont nommées différemment.

### Variables
* Une variable est un artifact hébergeant des données.
* Elle possède un nom.
* Elle possède un type.

### types
* Les données sont stockées sous différents formats : les types.
* Il existe plusieurs catégories de types :
    * Les types primitifs
    * Les énumérations
    * Les tableaux
    * Les enregistrements

* Tous les types déclarés possèdent un nom différent.

#### Tableaux
    * Un tableau possède unn type (qui peut être un autre tableau).
    * Un tableau définit une séquence de valeurs.
    * Toutes les valeurs d'un tableau ont le même type.
    * Un tableau possède au moins une dimension.
    * La dimension d'un tableau doit être strictement positive.

#### Enregistrement
    * Un enregistrement est un ensemble de valeurs groupées sous un même artifact.
    * Les valeurs d'un enregistrement peuvent être de différents types.
    * Un enregistrement doit avoir au moins un attribut.
    * Tous les attributs d'un même enregistrement doivent être nommés différemments.

#### Énumeration
* Une énumération est un type particulier de données.
* Il définit un nombre limité de valeurs (litéraux) propres.
* Tous les litéraux d'une énumération doivent être différents.

### Modules
* Un module est un élément réutilisable composé
  * de variables locales ;
  * de paramètres optionels en entrée ;
  * d'un retour optionel ;
  * d'un corps.

* Un module possède un nom.
* Un module peut utiliser les variables globales de la stratégie à laquelle il appartient.
* Toutes les paramètres au sein d'un module sont nommées différemment.
* Toutes les variables au sein d'un module sont nommées différemment.
* Une variable locale ne peut avoir le même nom qu'une variable globale.

### Objectifs
* Un objectif donne une orientation aux actions d'un personnage.
* Un objectif peut avoir plusieurs portées :
    * Court terme, en réaction à des stimulis de l'environnement.
    * Long terme, en toute généralité.
* Un objectif a une priorité implicite.
* Un objectif est caractérisé par une cible :
    * Néant (Random) - déplacements aléatoires.
    * AllerVers (Goto) - déplacements ciblés.
    * Contourner (Avoid) - déplacement ciblé autour d'un élément.
    * Éviter (Evade) - déplacement ciblé autour d'un personnage.
    * CollecterMax (Collect) - Ramassage d'objets.
    * Combattre (Attack) - attaque de personnages.
* Un objectif peut uniquement être changé au moyen d'une action Changer.
* Un objectif répond à une série de règles.
* Un objectif a nécessairement une règle par défaut.
* Un objectif a une priorité implicite (Court-terme > Long-terme)
* Si l'objectif long-terme est Random, alors l'objectif court-terme est long-terme.

### Règles
* Une règle est l'ensemble des actions qu'un personnage peut mettre en place pour réaliser un objectif.
* Une règle est composée
    * d'une priorité explicite.
    * d'un déclencheur (trigger)
    * d'une réaction (reaction)

* Une règle est
    * soit une règle normale.
    * soit une méta-règle.

* Un déclencheur est une expression booléenne.
* Une réaction est un artifact possédant
    * des variables ;
    * une séquence d'instruction.

* La règle par défaut d'un objectif a la priorité zéro.
=> la valeur de la priorité est inversément proportionnelle à son rang.
* Seule une métarègle possède une action de type Changer.
* Une séquence d'actions ne peut compter qu'une seule action de type movement.

### Expressions
* Une expression est un artifact permettant de représenter des données.
* Un expression peut être de différents types :
    * Litéral - un objet auto-exprimé.
    * Unaire - Un opérateur unaire lié à un expression.
    * Binaire - Un opérateur binaire lié à deux expressions.
    * Appel de module - un appel à un module prenant (ou non) des paramètres et produisant (ou non) un retour.
    * LHS - un élément de la mémoire pouvant être assigné ou récupéré.
    * Parenthésée - Un groupe d'expressions

### Instructions
* Une instruction est un fragment de programme.
* Elle permet
    * de manipuler les données et
    * d'effectuer des opérations : mouvements, interactions.
* Une instruction peut être de différents types :
    * Saut (Skip) - une instruction sans effet.
    * Conditionnelle (Selection) - une instruction de branchement, composée d'une garde et de 1 ou 2 branches (if...then...else...).
    * Itération (Iteration) - une instruction de répétition, composée d'une garde de sortie et d'un corps d'instruction.
    * Séquence (sequence) - une instruction composée d'une suite d'instructions.
    * Affectation (Assignment) - une instruction plaçant une valeur résultant d'une expression dans un symbole.
    * Action (Action) - une instruction réalisant une action.
