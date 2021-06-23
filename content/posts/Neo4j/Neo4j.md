---
layout:     post
title:      "CQL Query Language -- Neo4j"
subtitle:   "图数据库的查询语言"
date:       2019-11-27
author:     "Hitchcock"
# header-img: "universe.jpg"
tags:
    - Neo4j
    - Graphic database
    - CQL
---

This document is summarized based on the introdcution of Neo4j in [W3Cschool](https://www.w3cschool.cn/neo4j/neo4j_cql_introduction.html)

## Neo4j CQL common order/clause:

1. ###CREATE

   #### 1.1 Used to create non-attar node; create a non-statistic node

   ### Grammar: CREATE (<node-name:<label-name>)

   <node-name>: node name to create

   <label-name>: node tag name

   #### 1.2 Used to create attractive node

   ### Grammar: CREATE(

   ​							<node-name>:<label-name>

   ​							{

   ​								<Property1-name>:<Property1-value>

   ​								......

   ​								<Propertyn-name>:<Propertyn-Value>

   ​							}								

   ### )

   Attr is a key-value pair. 

   ### 1.3 Used to create one label for node

   ###       Used to create multiple labels for node

   Grammar: CREATE (<node-name>:<label-name1>:<label-name2>......:<label-name>)

   ###       Used to create one label for relation

   Grammar: CREATE(<node1-name>:<label1-name>)-[(<relationship-name>:<relationship-label-name>)]—>(<node2-name>:<label2-name>)

   

2. ### MATCH

   Used to achieve data related to nodes and attrs;

   Used to achieve data related to nodes, relations and attrs.

   ### Grammar: MATCH(

   ​								<node-name>:<label-name>

   )

3. ### RETURN

   Used to retrieve some attrs of node;

   Used to retrieve all attrs of node;

   Used to retrieve some attrs of node and relations;

   Used to retrieve all attrs of node and relations

   ### Grammar: RETURN

   ​							<node-name>.<property1-name>,

   ​							.......

   ​							<node-name>.<propertyn-name>

   **Concat 'Match' and 'Return'** to retrieve

   E.G. MATCH(dept: Dept)

   ​       RETURN dept.deptno, dept.dname

4. ### WHERE

5. ### DELETE

6. ### REMOVE

7. ### ORDER BY

8. ### SET



##  RELATION

**Unilateralism**

**Bilateralism**

