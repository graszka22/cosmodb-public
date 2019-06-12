Gdzie można za darmo pobawić się bazami Cosmos DB:
https://azure.microsoft.com/en-us/try/cosmosdb/

## SQL API

1. Stwórz nowy kontener SQL API
2. Stwórz nowy dokument za pomocą data explorera
3. Zaimportuj bazę pokemonów
4. Wyszukaj pokemona o imieniu Pikachu

`SELECT * FROM c WHERE c.name = "Pikachu"`

5. Wyszukaj wszystkie pokemony które mają typ Poison

`SELECT * FROM c JOIN type IN c.type WHERE type='Poison'`

6. Wypisz posortowane nazwy pokemonów

`SELECT c.name FROM c ORDER BY c.name`

7. Podaj średni `spawn_chance`

`SELECT VALUE AVG(c.spawn_chance) FROM c`

8.  Dla każdego pokemona wypisz jego imie i liste imion jego rewolucji, przykładowe wyjście: (\*?)

        `

    [
    {
    "name": "Vileplume",
    "evolutions": [
    "Oddish",
    "Gloom"
    ]
    },
    {
    "name": "Victreebel",
    "evolutions": [
    "Bellsprout",
    "Weepinbell"
    ]
    },
    {
    "name": "Tentacruel",
    "evolutions": [
    "Tentacool"
    ]
    },
    `

`SELECT c.name, ARRAY(SELECT VALUE p.name FROM p IN c.prev_evolution) AS evolutions FROM c`

9. Zobacz jak połączyć się z bazą w pythonie.
10. Rozprosz aplikację na kilka regionów, zobacz consistency levels.

## Table API

1. Stwórz nowa bazę Table API
2. Zobacz jak dodaje się dane w Data Explorer
3. Zobacz jak się robi zapytania w Data Explorer

## Gremlin

1. Stwórz nową bazę Gremlin db
2. Stwórz kilka wierzchołków

```
g.addV('person').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44).property('userid', 1)
g.addV('person').property('firstName', 'Mary Kay').property('lastName', 'Andersen').property('age', 39).property('userid', 2)
g.addV('person').property('firstName', 'Robin').property('lastName', 'Wakefield').property('userid', 3)
g.addV('person').property('firstName', 'Jack').property('lastName', 'Connor').property('userid', 5)
```

3. Stwórz kilka krawędzi

```
g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Mary Kay'))
g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Robin'))
g.V().hasLabel('person').has('firstName', 'Robin').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Ben'))
```

4. Wypisz ludzi którzy mają więcej niż 40 lat

`g.V().hasLabel('person').has('age', gt(40))`

5. Wypisz ich imiona

`g.V().hasLabel('person').has('age', gt(40)).values('firstName')`

6. Wypisz wszystkich przyjaciół Thomasa

`g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person')`

7. Wypisz przyjaciół przyjaciół Thomasa

`g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')`
