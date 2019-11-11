
# Filtering and Ordering - Lab


## Introduction
In this lab, you will write more `SELECT` statements to solidify your ability to query a SQL database. You will also write more specific queries using the tools you learned in the previous lesson.

## Objectives
You will be able to:
* Write SQL queries to filter and order results
* Order the results of your queries by using `ORDER BY` (`ASC` & `DESC`)
* Limit the number of records returned by a query using `LIMIT`
* Filter results using `BETWEEN` and `IS NULL`

### Famous Dogs

Here's a database full of famous dogs!  The `dogs` table is populated with the following data:

|name      |age    |gender |breed           |temperament|hungry |
|----------|-------|-------|----------------|-----------|-------|
|Snoopy    |3      |M      |beagle          |friendly   |1      |
|McGruff   |10     |M      |bloodhound      |aware      |0      |
|Scooby    |6      |M      |great dane      |hungry     |1      |
|Little Ann|5      |F      |coonhound       |loyal      |0      |
|Pickles   |13     |F      |black lab       |mischievous|1      |
|Clifford  |4      |M      |big red         |smiley     |1      |
|Lassie    |7      |F      |collie          |loving     |1      |
|Snowy     |8      |F      |fox terrier     |adventurous|0      |
|NULL      |4      |M      |golden retriever|playful    |1      |

## Connecting to the Database

First, import sqlite3 and establish a connection to the database **dogs.db**. Then, create a cursor object so that you can pass SQL queries to the database.


```python
#Your code here; import sqlite, create a connection and then a cursor object.
import sqlite3 
import pandas as pd
conn = sqlite3.connect('dogs.db')
cur = conn.cursor()
```

 

## Queries

Display the outputs for each of the following query descriptions.

### Select the name and breed for all female dogs


```python
cur.execute("""SELECT name, breed FROM dogs
                WHERE gender = 'F';""").fetchall()

```




    [('Little Ann', 'coonhound'),
     ('Pickles', 'black lab'),
     ('Lassie', 'collie'),
     ('Snowy', 'fox terrier')]



### Select the names of all dogs listed in alphabetical order.  Notice that SQL lists the nameless dog first.


```python
cur.execute("""SELECT name FROM dogs
                ORDER BY name ASC;""").fetchall()
```




    [(None,),
     ('Clifford',),
     ('Lassie',),
     ('Little Ann',),
     ('McGruff',),
     ('Pickles',),
     ('Scooby',),
     ('Snoopy',),
     ('Snowy',)]



### Select any dog that doesn't have a name


```python
cur.execute("""SELECT name FROM dogs
                WHERE name IS NULL;""").fetchall()
```




    [(None,)]



### Select the name and breed of only the hungry dogs and list them from youngest to oldest


```python
cur.execute("""SELECT name, breed FROM dogs
                WHERE temperament = 'hungry'
                ORDER BY age ASC;""").fetchall()
```




    [('Scooby', 'great dane')]



### Select the oldest dog's name, age, and temperament


```python
cur.execute("""SELECT name, age, temperament FROM dogs
                ORDER BY age DESC LIMIT 1;""").fetchall()
```




    [('Pickles', 13, 'mischievous')]



### Select the three youngest dogs


```python
cur.execute("""SELECT * FROM dogs ORDER BY age ASC LIMIT 3;""").fetchall()
```




    [(1, 'Snoopy', 3, 'M', 'beagle', 'friendly', 1),
     (6, 'Clifford', 4, 'M', 'big red', 'smiley', 1),
     (9, None, 4, 'M', 'golden retriever', 'playful', 1)]



### Select the name and breed of the dogs who are between five and ten years old, ordered from oldest to youngest


```python
cur.execute("""SELECT name, breed FROM dogs
                WHERE age BETWEEN 5 and 10
                ORDER BY age DESC;""").fetchall()
```




    [('McGruff', 'bloodhound'),
     ('Snowy', 'fox terrier'),
     ('Lassie', 'collie'),
     ('Scooby', 'great dane'),
     ('Little Ann', 'coonhound')]



### Select the name, age, and hungry columns for hungry dogs between the ages of two and seven.  This query should also list these dogs in alphabetical order.


```python
cur.execute("""SELECT name, age, hungry FROM dogs
                WHERE hungry = 1 AND age BETWEEN 2 and 7
                ORDER BY name ASC;""").fetchall()
```




    [(None, 4, 1),
     ('Clifford', 4, 1),
     ('Lassie', 7, 1),
     ('Scooby', 6, 1),
     ('Snoopy', 3, 1)]



## Summary

Great work! In this lab you practiced writing more complex SQL statements to not only query specific information but also define the quantity and order of your results. 
