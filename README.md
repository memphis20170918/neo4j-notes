# neo4j-notes

* Create nodes and relationships.

```shell
CREATE (p:Router {name: "node1"}) - [:Neighbor {parent: "node1", child: "node2"}] -> (c:Router {name: "node2"});
0 rows available after 345 ms, consumed after another 0 ms
Added 2 nodes, Created 1 relationships, Set 4 properties, Added 2 labels
```

* Specify constraints.

CREATE CONSTRAINT ON (router: Router) ASSERT router.name IS UNIQUE;

- list all rows in the default database.

MATCH (n) RETURN n;
+---------------------------------+
| n                               |
+---------------------------------+
| (:Router {name: "node1"})       |
| (:Router {name: "node2"})       |
+---------------------------------+

2 rows available after 3 ms, consumed after another 5 ms
