## Elasticseach, le fonctionnement

[:arrow_left: Revenir au concepts](./README.md)

## Opérations basic [CLI avec curl]

**Lancez elasticsearch et elasticsearch-head (pour la visualisation)**

![1](./screeshots/operations/1.JPG)

![2](./screeshots/operations/2.JPG)

#### Création d'un index

La première opération à effectuer avant de commencer à indexer des données dans Elasticsearch est de créer un index - le conteneur principal de nos données.

Un index est similaire au concept de base de données en SQL, un conteneur pour les types (tables en SQL) et les documents (enregistrements en SQL).

the HTTP method to create an index is PUT (but also POST works); the REST URL contains the index name:

`http://<server>/<index_name>`

**Création d'un Index**

```bash
curl -XPUT http://localhost:9200/bdcc_index1 '{"settings":{"index":{"number_of_shards" : 2,"number_of_replicas" : 1}}}' -H'Content-Type: application/json'

```

Resultat :

![](./screeshots/operations/3.JPG)

L'option `-H'Content-Type: application/json'` est important pour spécifier le type de contenue de la requête: plus d'information sur ([plus d'informations ? :hand:](https://www.elastic.co/blog/strict-content-type-checking-for-elasticsearch-rest-requests))

Exemple d'erreur dans le nom de l'index :

![4](./screeshots/operations/4.JPG)

Si l'Index exist déja, la commande va générer une erreur `404`.

![5](./screeshots/operations/5.JPG)

**Noter**: Comme le nom de l'index sera mappé sur un répertoire de votre stockage, il y a quelques limitations au nom de l'index, et les seuls caractères acceptés sont :

- les lettres ASCII [a-z]
- Chiffres [0-9]
- Point ".", moins "-", "&" et "\_".

Pendant la création de l'index, la réplication peut être définie avec deux paramètres dans l'objet settings/index :

- number_of_shards, qui contrôle le nombre de shards qui composent l'index (chaque shard peut stocker jusqu'à 2^32 documents)
- number_of_replicas, qui contrôle le nombre de répliques (combien de fois vos données sont répliquées dans le cluster pour une haute disponibilité). Une bonne pratique consiste à fixer cette valeur à au moins 1.
  L'appel API initialise un nouvel index, ce qui signifie :

- L'index est d'abord créé dans un nœud primaire, puis son statut est propagé à tous les nœuds du niveau cluster.
- Un mappage par défaut (vide) est créé
- Tous les shards requis par l'index sont initialisés et prêts à accepter des données.

On peut voir l'index par `elsticsearch-head`

![6](./screeshots/operations/6.JPG)

**Création d'un index en utilisant elsticsearch-head**

![7](./screeshots/operations/7.JPG)

![8](./screeshots/operations/8.JPG)

![8](./screeshots/operations/9.JPG)

[//]: <> (This is a comment )
[comment]: <> (This is a comment )

**Suppression d'un index**

La suppression d'un index signifie la suppression de ses shards, mappings et données.

[:arrow_left: Revenir au concepts](./README.md)

### Next Section: [Comming soon:arrow_right:](./concepts.md)
