# Hello, Neo4j

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

Node with 2 labels

```python
CREATE (n:Person:Indian)
```

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

```python
MATCH (n:Person), (m:Person)
CREATE (n)-[:SOME_RELATIONSHIP]->(m)
```

```python
MATCH (n:Person {name: "Hello World"}), (m:Person {name: "Kan Ouivirach"})
CREATE (n)-[:SOME_RELATIONSHIP]->(m)
```

Flow การซื้อขายของจากระบบๆ หนึ่ง

```python
CREATE (:User {name: "Newy", address: "Here 1234"})
```

เซิชหา Product โดยชื่อ

```python
MATCH (n:Product)
WHERE n.name CONTAINS "แก้ว"
RETURN n
LIMIT 4
```

ถ้าอยากจะดูของในหมวด Category นั้นๆ

```python
MATCH (:Product)->[:IS_CAT]->(c:Category {name: "เสื้อผ้า"})
RETURN p
```

ด้านบนเราจะได้ Node ที่ชื่อว่า "เสื้อผ้า" แต่จริงๆ เราอยากได้ Node ที่เชื่อมต่อกับ Node นี้ทั้งหมด

```python
MATCH (d:Category)-[:SUBCAT]->(c:Category {name: "เสื้อผ้า"})
RETURN d
```

ด้านบนจะได้ลูกของ "เสื้อผ้า" โดยตรง

```python
MATCH (d:Category)-[:SUBCAT*0..2]->(c:Category {name: "เสื้อผ้า"})
RETURN d
```

ด้านบนจะได้ที่เชื่อมโยงกับเสื้อผ้ามา 2 ชั้น หรือเราจะกำหนดกี่ชั้นก็ได้ตามนี้

```python
MATCH (d:Category)-[:SUBCAT*0..]->(c:Category {name: "เสื้อผ้า"})
RETURN d
```

ทีนี้ถ้าเราอยากได้ Product

```python
MATCH (p:Product)-[:IS_CAT]->(d:Category)-[:SUBCAT*0..]->(c:Category {name: "เสื้อผ้า"})
RETURN p
```

ถ้าเราอยากเห็น Category ด้วย ก็เพิ่ม d ใน RETURN

```python
MATCH (p:Product)-[:IS_CAT]->(d:Category)-[:SUBCAT*0..]->(c:Category {name: "เสื้อผ้า"})
RETURN d, p
```

Delete a relationship

```python
MATCH ()-[r:SOME_RELATIONSHIP]->(n) DELETE r
```

Delete a node

```python
MATCH (n) WHERE id(n) = 1 DELETE n
```

```python
MATCH (n) WHERE id(n) IN [1, 2] DELETE n
```

Delete all nodes

```python
MATCH (n) DELETE n
```

Set label to node

```python
MATCH (n) SET n:Employeee RETURN n
```

```python
MATCH (n) WHERE id(n) = 0 SET n:Manager RETURN n
```

Remove label

```python
MATCH (n) REMOVE n:Person RETURN n
```

```python
MATCH (n) WHERE id(n) = 2 REMOVE n:Employee RETURN n
```

ดูว่ามี labels อะไรบ้าง

```python
MATCH (n) RETURN DISTINCT labels(n)
```

ดูว่าแต่ละ labels มีจำนวนเท่าไหร่

```python
MATCH (n) RETURN DISTINCT count(labels(n)), labels(n)
```

ลบโหนดจาก labels

```python
MATCH (n) WHERE n:TeamLeader DELETE n
```

สร้างโหนดกับ properties

```python
CREATE (x:Book {title: "The White Tiger"}) RETURN x
```

Search

```python
MATCH (n:Book) WHERE n.price < 1000 RETURN n
```

Update property

```python
MATCH (n) WHERE n.title = "Last man" SET n.title = "Last Man", n.price = 99 RETURN n
```