# neo4j-notes

* Create the `Router` and `Neighbor` nodes.

```shell
neo4j> CREATE (:Router {name: "node1"}), (:Router {name: "node2"});
0 rows available after 44 ms, consumed after another 0 ms
Added 2 nodes, Set 2 properties, Added 2 labels
```
```shell
neo4j> CREATE (:Neighbor {parent: "node1", child: "node2"}); 
0 rows available after 39 ms, consumed after another 0 ms
Added 1 nodes, Set 2 properties, Added 1 labels
```

* Create the relationship connecting `node1` and `node2`.
```shell
CREATE (p:Router {name: "node1"}) - [:Neighbor {parent: "node1", child: "node2"}] -> (c:Router {name: "node2"});
0 rows available after 345 ms, consumed after another 0 ms
Added 2 nodes, Created 1 relationships, Set 4 properties, Added 2 labels
```

* Specify constraints.
```shell
CREATE CONSTRAINT ON (router: Router) ASSERT router.name IS UNIQUE;
```

- List all rows in the default database.
```shell
MATCH (n) RETURN n;
+---------------------------------+
| n                               |
+---------------------------------+
| (:Router {name: "node1"})       |
| (:Router {name: "node2"})       |
+---------------------------------+
```

2 rows available after 3 ms, consumed after another 5 ms

* Adding constraints.

```shell
neo4j> CREATE CONSTRAINT ON (router: Router) ASSERT router.name IS UNIQUE; 
0 rows available after 458 ms, consumed after another 0 ms
Added 1 constraints
```

* Delete a node.
```shell
neo4j> match (r:Router {name: "node1"}) delete r;
0 rows available after 151 ms, consumed after another 0 ms
Deleted 1 nodes
```
```shell
neo4j> match (n:Neighbor {parent: "node1", child: "node2"}) delete n;
0 rows available after 103 ms, consumed after another 0 ms
Deleted 1 nodes
```

* View the graph.
```shell
neo4j> MATCH (r1:Router)-[n]-(r2) RETURN r1, n, r2;
+---------------------------------------------------------------------------------------------------------------------------+
| r1                              | n                                                     | r2                              |
+---------------------------------------------------------------------------------------------------------------------------+
| (:Router {name: "node1"})       | [:Neighbor {parent: "node1", child: "node2"}]         | (:Router {name: "node2"})       |
| (:Router {name: "node2"})       | [:Neighbor {parent: "node1", child: "node2"}]         | (:Router {name: "node1"})       |
+---------------------------------------------------------------------------------------------------------------------------+

2 rows available after 127 ms, consumed after another 18 ms
```
```shell
neo4j> MATCH (parent:Router)-[n]->(child) RETURN parent, neighbor, child;
+-----------------------------------------------------------------------------------------------------------------------+
| parent                      | neighbor                                              | child                           |
+-----------------------------------------------------------------------------------------------------------------------+
| (:Router {name: "node1"})   | [:Neighbor {parent: "node1", child: "node2"}]         | (:Router {name: "node2"})       |
+-----------------------------------------------------------------------------------------------------------------------+

1 row available after 60 ms, consumed after another 1 ms
```
