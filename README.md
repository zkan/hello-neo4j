# Hello, Neo4j

## CREATE

Create a new node

```python
CREATE (n)
```

Create 2 nodes

```python
CREATE (n), (m)
```

Create a node with label

```python
CREATE (n:Person)
```

Create a node with label and properties
```python
CREATE (:Person {name: "Kan Ouivirach"})
CREATE (:Person {name: "Hello World"})
```

```python
CREATE (:User {name: "Newy", address: "Here 1234"})
```

```python
CREATE (x:Book {title: "The White Tiger"}) RETURN x
```

Create a node with 2 labels

```python
CREATE (n:Person:Indian)
```

## MATCH

View and search the nodes

```python
MATCH (n) RETURN n
```

```python
MATCH (n) RETURN n limit 2
```

```python
MATCH (n) WHERE id(n) = 1 RETURN n
```

```python
MATCH (n) WHERE id(n) <= 6 RETURN n
```

```python
MATCH (n) WHERE id(n) IN [1, 2, 0] RETURN n
```

```python
MATCH (n) WHERE n:Person RETURN n
```

```python
MATCH (n) WHERE n:Person:Indian RETURN n
```

```python
MATCH (n) WHERE n:Person OR n:Indian RETURN n
```

Create a relationship between nodes

```python
MATCH (n:Person), (m:Person)
CREATE (n)-[:SOME_RELATIONSHIP]->(m)
```

```python
MATCH (n:Person {name: "Hello World"}), (m:Person {name: "Kan Ouivirach"})
CREATE (n)-[:SOME_RELATIONSHIP]->(m)
```

```python
MATCH (n:Product)
WHERE n.name CONTAINS "แก้ว"
RETURN n
LIMIT 4
```

```python
MATCH (:Product)->[:IS_CAT]->(c:Category {name: "เสื้อผ้า"})
RETURN p
```

```python
MATCH (d:Category)-[:SUBCAT]->(c:Category {name: "เสื้อผ้า"})
RETURN d
```

```python
MATCH (d:Category)-[:SUBCAT*0..2]->(c:Category {name: "เสื้อผ้า"})
RETURN d
```

```python
MATCH (d:Category)-[:SUBCAT*0..]->(c:Category {name: "เสื้อผ้า"})
RETURN d
```

```python
MATCH (p:Product)-[:IS_CAT]->(d:Category)-[:SUBCAT*0..]->(c:Category {name: "เสื้อผ้า"})
RETURN p
```

We can return more than one:

```python
MATCH (p:Product)-[:IS_CAT]->(d:Category)-[:SUBCAT*0..]->(c:Category {name: "เสื้อผ้า"})
RETURN d, p
```

Search

```python
MATCH (n:Book) WHERE n.price < 1000 RETURN n
```

Show the labels

```python
MATCH (n) RETURN DISTINCT labels(n)
```

Show the number of nodes in each label

```python
MATCH (n) RETURN DISTINCT count(labels(n)), labels(n)
```

## SET

Set label to node

```python
MATCH (n) SET n:Employeee RETURN n
```

```python
MATCH (n) WHERE id(n) = 0 SET n:Manager RETURN n
```

Update property

```python
MATCH (n) WHERE n.title = "Last man" SET n.title = "Last Man", n.price = 99 RETURN n
```

## REMOVE

Remove label

```python
MATCH (n) REMOVE n:Person RETURN n
```

```python
MATCH (n) WHERE id(n) = 2 REMOVE n:Employee RETURN n
```

ลบโหนดจาก labels

```python
MATCH (n) WHERE n:TeamLeader DELETE n
```

## DELETE

Delete a node

```python
MATCH (n) WHERE id(n) = 1 DELETE n
```

Delete a relationship

```python
MATCH ()-[r:SOME_RELATIONSHIP]->(n) DELETE r
```

```python
MATCH (n) WHERE id(n) IN [1, 2] DELETE n
```

Delete all nodes

```python
MATCH (n) DELETE n
```