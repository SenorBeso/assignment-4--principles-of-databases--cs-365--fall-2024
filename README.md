# Fall 2024 Principles of Databases — Assignment 4

* **Do not start this project until you’ve read and understood these instructions. If something is not clear, ask.**

---

## ❖ Introduction ❖

For this assignment, you will write responses to nine questions based on different topics from our textbook, *Database Systems — The Complete Book* and to one question based on your notes. Reply to each question in the provided region using Markdown syntax.

---

## ❖ Questions ❖

### 1. [2.4] What is the difference between a Cartesian Product, a Natural Join, and Theta-Joins?
The difference in these three is the way that they are paired:

A cartesian product is the algebraic operation of two sets (R and S) that pairs the first element of R, with any second element S. The result is called R x S. The resulting relation is the union of the two relations, and combines every element of R with with all elements of S. In addition, if there is attributes in common between the two, we need to invent new names for them, as it would be a conflict. The result is in dot notation, with the attribute (X) being the name after that dot, i.e. R.X, and S.X, so we can differentiate between the common attribute from R and S.

A natural join is when there is two relations, and the tuples between the two are paired when they have values that match on those common attributes, and have the same values in the tuple. This means that since the result will be unique, there is no need for the dot notation that is used with the cartesian product.

Finally, theta-joins are similar to natural joins by pairing relations, but the condition they are paired on is not the common attribute, but some other condition that can be chosen, which allows for some other options, albeit less common than natural join. The final relation is then joined upon the conditions chosen, and is those tuples, using dot notation similar to cartesian products.


### 2. [2.5] What is a Referential Integrity Constraint?

A referential integrity constraint is when a value in one relation has to appear in some other relation, that is is "related" in some fashion. It ensures the relationship and makes sure that information is consistent between the two. It is similar if there is a parent table, and there were dependent children tables. If something was deleted in the parent, the dependent children tables would have dangling tuples in the child table. This can be used in foreign key relationships, where the foreign key should match a the primary key value in the other relation, avoiding dangling tuples.

###  3. [2.5] What is a Key Constraint?

A key constraint is when no rows of a table can have the same attribute value (in the specified attribute), to ensure that there is uniqueness among this attribute. This would be the primary key(s) of this relation. If it is designated as a primary key, then no tuples will have the same value in the specified key attribute. An example would be for enrolling for classes, each class has a unique CRN, which would be the primary key constraint for the classes relation.

### 4. [4.1] What is an Entity/Relationship Model? What purpose does it serve in the process of creating/designing databases?

An entity/relationship model is a way of visually representing a relational database, composed of three parts. The first part is all of the Entity sets, which are the relations or tables. These in an E/R diagram are represented as rectangles. The second part is the relationships between entity sets, which are represented as diamonds. Finally, the attributes of the entity sets are represented as ovals, connected to the entity set rectangles. The diamond relationships connect entity sets. Attributes can also be modeled by underlining the attribute in the oval to represent primary keys. Similarly, we can represent different relation ship types, with arrows between the entity sets and relationship diamonds, to show many to one relationships. The purpose it serves is a jumping off point to start in SQL, as the diagram can easily be implemented into MySQL, and help to design the database on paper before you get started.

### 5. [4.4] What is a Weak Entity Set?

A weak entity set is when the key of the weak entity set is a part of another entity set. In essence this means that primary key of the "other" entity set, which is a foreign key, is the this entity set's primary key. The relationship needs to have referential integrity. This relationship also needs to be a many to one relationship, as well as binary, and can be denoted as a double bordered rectangle in the E/R diagram. The weak entity set has to have zero or more attributes of its own, and key attributes from the other entity set (which is considered the strong entity set).

### 6. [5.2.7; 6.3.8] Explain the concepts of Outerjoin, Natural Right Outer Joins, Natural Left Outer Joins, and Full Outer Joins.

An outerjoin is when we do a natural or theta join, but any of the dangling tuples that may have occurred are included in the joined relation. When this occurs, any attribute that was dangling is given a null value, and as mentioned are included in the output relation. The difference with Natural Right outerjoins and Natural Left outerjoins is that they do the same thing, except if it is a right, only the dangling tuples that are on the right relation are included, and a left only includes the dangling tuples from the left relation in the join statement. A full outer join is the same as an outer join, and includes the dangling tuples from both of the relations.

### 7. [6.6.3] What is the difference between the SQL command `TRANSACTION` and the execution of any statement in SQL?

The difference between them is that the execution of any statement isolated by itself is atomic, and each statment is independent of the others. However, with TRANSACTION, we can group statements together to be atomic, and have to be all or nothing within the grouped statements. These transactions have to end with either ROLLBACK, or COMMIT. If the group finishes successfully, we make the permanent change to the database with COMMIT. If something in the group fails, we ROLLBACK, which reverts any of the changes made during the statements executed within the TRANSACTION grouping.

### 8. [8] What is a Virtual View and what are its advantages?

A virtual view is a relation that was created by a query that is based off of a relation. They can be created with this statement, CREATE VIEW (name) AS query; The views will not physically exist and will be deleted when the session is over, however can be queried while the session is active, and can be modified in certain circumstances. The modifications will be stored, but not the view itself. One advantage is that it can make a long sequence of queries into a simpler one that can be continually referenced during the session. These are also helpful because it helps to isolate the actual relation, and not allow users to interact with data in the relation that they should not see, or be able to modify, for example a primary key value like a bank account number of other members of the bank.

### 9. [8.3] What is an *index* and what are its advantages?

An index is a something that can be assigned to an attribute, typically the most queried attribute of the database, or primary keys. What it does is it can speed up the retrieval of data, and therefore quereies, on a table. This is done by reducing what has to be parsed, as it is not searching on the entire tuple, but on the indices. However, having too many indices, or attributes that are indexes, will become more inefficient, so it is best practice to have as few indexes as possible. An index is created by the statement CREATE INDEX name ON TableName(nameOfAttribute).

### 10. Explain the concept of an MVC, or model, view, controller, framework for designing full stack applications

A MVC is the design structure/framework that can separate a project/app into three parts, that interact with one another.

The view layer is the component that is the visual representation of the project/app. This is the part that a user would "view" and interact with, like a GUI. Views then interact with the middle layer, the Controller, like HTML or CSS for example.

The controller is the middle man, that will interact with both the view and the model. What it does is it will convert and take any input from the view layer that the user did, and then interact with the model to make the modifications. The controller is what enables the separation, so the user is not directly interacting with the model, like PHP for example.

The model is the actual data of the project/application. This is where the information is stored, manipulated, and where something like a database management system is, like SQL. The user cannot interact with this component, only the controller, which has already translated the users actions to correctly interact with the model.

By segmenting these three layers, we can create a framework that allows independent changes to be made to each layer, without affecting the other parts. This full stack framework ensures the security of the model, the independence of the user from the model, and the designated actions the view has to convert user interactions to access the model.

---

## ❖ Due ❖

Sunday, 15 December 2024, at 10:00 AM.

---

## ❖ Grading ❖

| Item        | Points |
|-------------|:------:|
| Question 1  | `10`   |
| Question 2  | `10`   |
| Question 3  | `10`   |
| Question 4  | `10`   |
| Question 5  | `10`   |
| Question 6  | `10`   |
| Question 7  | `10`   |
| Question 8  | `10`   |
| Question 9  | `10`   |
| Question 10 | `10`   |

---

## ❖ Submission ❖

**NO late submissions will be accepted.**

You will need to issue a pull request back into the original repo, the one from which your fork was created for this project. See the **Issuing Pull Requests** section of [this site](http://code-warrior.github.io/tutorials/git/github/index.html) for help on how to submit your assignment.

**Note**: This assignment may **only** be submitted via GitHub. **No other form of submission will be accepted**.
