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

3. Expliquez ce que vous comprenez des différentes étapes de simplification implémentées (fichier src/simplification/simplify.cpp) et les raisons pour lesquelles elles sont utilisées (leur impact sur la structure du graphe, les avantages/inconvénients, etc.).
