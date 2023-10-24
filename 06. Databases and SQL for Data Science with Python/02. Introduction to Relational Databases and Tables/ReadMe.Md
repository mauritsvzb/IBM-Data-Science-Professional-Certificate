# Introduction to Relational Databases and Tables

## Relational Database Concepts

### Relational Model
Data is stored in tables. This provides logical data independence, physical data independence, and physical storage independence.

### Entity-Relationship (ER) Model
ER models are used as a tool to design relational databases. The building blocks of an ER diagram are entities and attributes.

Entities are drawn as rectangles, and attributes as ovals, as shown below.

<img src="https://user-images.githubusercontent.com/13508894/277740356-01b3af8e-3227-4f7a-a221-6075c6fd17c2.png" width="500" />

A database can be thought of as a collection of entities, rather than being used as a model on its own. Entities are objects that independently of any other entities in the database (that have attributes).

In the above example, each attribute is connected to exactly one entity (Book), so this will become a table in the database, and the attributes will be the columns.

In an ER model:

* ENTITIES map to TABLES in a relational database
* ATTRIBUTES map to COLUMNS in a table
* A PRIMARY KEY uniquely identifies a specific row in a table.

## Types of SQL statements (DDL vs. DML)
SQL Statements are used for interacting with entities (tables), attributes (columns), and their tuples (or rows with data values) in relational databases. SQL statements fall into two different categories:

* Data Definition Language (DDL) statements
* Data Manipulation Language (DML) statements

### DDL Statements
Used for creating tables and defining its columns:
```
CREATE TABLE table_name (
  column1 datatype,
  column2 datatype,
  column3 datatype,
  ....
);
```
