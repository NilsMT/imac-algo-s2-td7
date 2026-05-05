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

1. Identifiez où sont définies les structures principales du graphe (WeightedGraph / PositionedGraph) et expliquez brièvement leur rôle et comment elles sont utilisées.

`WeightedGraph` est situé dans `src/dataStructure`

> il sert à avoir des poids associé à chaque noeud du grave via `adjency_list` qui associe une ID de noeud à une liste de voisins (`std::vector<WeightedArc>`) et `WeightedArc` contient un poids (`weight`) et le noeud qu'il pointe (`to`)
>
> ℹ️ c'est donc un graphes pondéré et orienté

`PositionedGraph` est situé dans `src/osm`

> il utilise `WeightedGraph` pour son graphe, cependant il utilise contient aussi la liste des noeuds avec ses coordonnées 2D (`std::unordered_map<OSM::NodeId, glm::vec2> nodes`)
>
> ℹ️ c'est donc un graphes pondéré et orienté avec la liste des positions (dans un espace 2D) des noeuds

1. Expliquez en quelques lignes le rôle des modules:

- extraction OSM,
- simplification,
- visualisation.

3. Expliquez ce que vous comprenez des différentes étapes de simplification implémentées (fichier src/simplification/simplify.cpp) et les raisons pour lesquelles elles sont utilisées (leur impact sur la structure du graphe, les avantages/inconvénients, etc.).
