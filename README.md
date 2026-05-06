# Exercice 1 - Prise en main du projet OSM

La commande

```
PS [...]\imac-algo-s2-td7\bin> ."E:/IMAC/S2/ProgAlgo/imac-algo-s2-td7/bin/imac-algo-s2-td7.exe" extract data/test.osm data/
```

Donne

```
test_extract.graph
Graph processing tool
Input path: data/test.osm
8043 nodes Loaded from OSM file.
1154 ways Loaded from OSM file.
```

# Exercice 2 - Lecture de code et compréhension

## Question 1

_Identifiez où sont définies les structures principales du graphe (WeightedGraph / PositionedGraph) et expliquez brièvement leur rôle et comment elles sont utilisées._

`WeightedGraph` est situé dans [src/dataStructure](./src/dataStructure)

> Il sert à avoir des poids associé à chaque noeud du grave via `adjency_list` qui associe une ID de noeud à une liste de voisins (`std::vector<WeightedArc>`) et `WeightedArc` contient un poids (`weight`) et le noeud qu'il pointe (`to`)

> ℹ️ C'est donc un graphes pondéré et orienté

`PositionedGraph` est situé dans [src/osm](./src/osm)

> Il utilise `WeightedGraph` pour son graphe, cependant il utilise contient aussi la liste des noeuds avec ses coordonnées 2D (`std::unordered_map<OSM::NodeId, glm::vec2> nodes`)

> ℹ️ C'est donc un graphes pondéré et orienté avec la liste des positions (dans un espace 2D) des noeuds

## Question 2

_Expliquez en quelques lignes le rôle des modules:_

- _extraction OSM,_
- _simplification,_
- _visualisation._

L'extraction OSM permet d'ouvrir les fichiers `.osm` et les transformer en `PositionedGraph` en filtrant pour ne conserver que es routes (donc pas de rails et de bâtiments)

La simplification reduit le nombres de connexions dans un graphe en fusionnant ceux qui sont très proches, et en conservant les plus grandes composants connexes

La visualisation permet de visualisé un graphe avec l'algorithme de djikstra, avec un zoom inclus dans la fenêtre et le fait de réinitialiser un noeud en cliquant dessus

## Question 3

_Expliquez ce que vous comprenez des différentes étapes de simplification implémentées (fichier src/simplification/simplify.cpp) et les raisons pour lesquelles elles sont utilisées (leur impact sur la structure du graphe, les avantages/inconvénients, etc.)._

1. On conserve les composantes connexes les plus larges pour optimisé le nombre de composantes enregistrées
2. Supprime les noeud avec un seul degré et proche de son voisin, pour fusionner les noeuds proches
3. Si A -> B et A -> C, alors autant faire B -> C, néanmoins on a une perte d'information en faisant ça
4. Si un groupe de noeud va vers un même voisin (d'après une certaine profondeur) alors on les fusionnes (= il font tous le même chemin), néanmoins on a une perte d'information en faisant ça
5. Réitère l'étape 3 car il y a eu un changement avec l'étape 4, donc on a aussi une perte d'information.
