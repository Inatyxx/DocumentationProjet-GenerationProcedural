# DocumentationProjet-GenerationProcedural

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Simple Room Placement :

  Principe :
    On génère une area en fond. Par-dessus, on essaye de placer une pièce : si l’espace est suffisant on la place, sinon on réessaie X fois avant d’abandonner.
    Ensuite, on relie les pièces entre elles avec des couloirs.
  
  Avantages :
    Simple d’utilisation
    Coûts d’exécution rapides
    Idéal pour des jeux de type donjon pas trop gros
  
  Inconvénients :
    Relier les salles peut vite devenir chaotique et créer beaucoup de couloirs qui s’entrecroisent
  
  Fonctions à retenir :
    PlaceRoom(RectInt) → permet de placer une pièce
    CanPlaceRoom() → permet de vérifier si on peut poser une pièce
    CreateDogLegCorridor(start, end) → permet de relier les pièces avec des couloirs
    CreateHorizontalCorridor / CreateVerticalCorridor → permet de tracer des couloirs
    BuildGround() → pose l’area

  Ex : <img width="679" height="387" alt="image" src="https://github.com/user-attachments/assets/46e48801-9b4e-4709-9da3-b9726a5bb681" />

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

BSP Trees :

  Principe :
    On part d’une area qui couvre toute la map.
    On choisit aléatoirement un split horizontal/vertical, puis on vérifie si la découpe est valide (taille minimale).
    Si oui → on crée deux enfants qu’on peut rediviser si souhaité.
    Quand on décide d’arrêter de split, on génère une salle dans la zone.
    Après la génération de l’arbre, on connecte les rooms d’un même niveau ensemble puis on remonte l’arbre en connectant avec les parents.
  
  Avantages :
    Permet de générer des donjons imposants sans qu’ils soient chaotiques
    Génération stable
  
  Inconvénients :
    Complexe à coder
    La disposition paraît moins “naturelle”
    Produit des layouts assez carrés / prévisibles
  
  Fonctions à retenir :
    Node.Split() → permet la découpe
    CanSplitHorizontally / Vertically → vérifie que la coupe est autorisée
    PlaceRoom(RectInt) → permet de placer une pièce
    ConnectSisters() → connecte les salles “sœurs” entre elles
    CreateDogLegCorridor(start, end) → relie deux pièces
    
  Ex : <img width="676" height="379" alt="image" src="https://github.com/user-attachments/assets/e7b81757-95f8-49c7-9523-0d2d6a19ee9b" />

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

Cellular AutoMata :

  Principe :
    On génère une grille complètement aléatoire, puis on fixe des règles qui influent sur l’état de la grille à l’étape suivante
    (ex : une cellule devient de l’herbe si 4 voisins ou plus sont de l’herbe).
    On parcourt alors la grille et on sauvegarde l’état futur de chaque case.
    Une fois la grille parcourue, on met la map à jour.
    On répète l’opération autant de fois que souhaité.
  
  Avantages :
    Produit des formes plutôt naturelles et organiques
    Adapté à des environnements naturels comme des archipels d’îles ou des réseaux de cavernes
    Facilement modulable en changeant les règles
    Assez facile à développer
  
  Inconvénients :
    Complètement imprévisible (basé sur le chaos)
    Inadapté à la génération de donjon
    Nécessite plusieurs mises à jour pour obtenir un résultat cohérent
  
  Fonctions à retenir :
    GenerateNoiseGrid(density) → remplit la grille avec un sol aléatoire
    ScanCell(cell) → compte les voisins pour déterminer si la case doit changer d’état ou non
    AddTileToCell(cell, type) → remplace la cellule par la nouvelle à cet emplacement
    _maxSteps → définit le nombre d’itérations de mise à jour de la grille

  Ex : <img width="678" height="383" alt="image" src="https://github.com/user-attachments/assets/7d0878e7-dbb2-46c8-96a6-3484dddedb08" />

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

FastNoiseLite :

  Principe :
    On utilise une fonction de noise (Perlin, OpenSimplex, Cellular, etc.) pour générer une hauteur entre -1 et 1 pour chaque cellule.
    Selon cette hauteur, on applique des seuils pour choisir le type de terrain
    (ex : [0, 0.3] = eau ; ]0.3, 0.6] = sable ; ]0.6, 1] = herbe).
  
  Avantages :
    Exécution très rapide
    Produit des formes plutôt naturelles et organiques
    Adapté à des environnements naturels comme des archipels d’îles ou des réseaux de cavernes
    Très facilement modulable grâce aux nombreux paramètres
    Très simple à utiliser avec la librairie officielle :
    https://github.com/Auburn/FastNoiseLite/blob/master/CSharp
  
  Inconvénients :
    Difficile à développer from scratch
  
  Fonctions à retenir :
    noise.SetNoiseType(type) → configure le type de bruit
    noise.SetFrequency(freq) → contrôle le niveau de détails
    noise.GetNoise(x, y) → renvoie la hauteur au point (x, y)
    Seuils : highWater, highSand, highGrass, highRock → déterminent les biomes (du plus bas au plus haut)
    AddTileToCell(cell, biomeName) → pose le terrain correspondant

  Ex : <img width="678" height="379" alt="image" src="https://github.com/user-attachments/assets/97e73544-782f-47fa-86e3-626fd5452f8d" />














































