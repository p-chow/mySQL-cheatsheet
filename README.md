# mySQL-cheatsheet
BT2102

### Integrity Control
Defining constraints on col/ table: 
`CHECK (SearchCondition)` eg. SEX CHAR NOT NULL CHECK (sex IN('M', 'F'))

### Creating/ dropping domain:
```
CREATE DOMAIN domainName [AS] datatype
 [DEFAULT defaultOption]
  [CHECK (SearchCondition)]
```
`DROP DOMAIN DomainName [RESTRICT|CASCADE]`

RESTRICT: if domain is used in existing table, drop fails
CASCADE: table columns dependent on domain will use underlying data type, domain consntraints replaced by column constraints

### Primary Key
define pri key: `PRIMARY KEY (attributeName)`

composite primary key: `PRIMARY KEY (key1, key2)`


## SELECT & FROM
#### selecting **max** : 
```
SELECT c1, c2 
  FROM tableName 
    WHERE c1 = (SELECT MAX (c1) 
                  FROM tableName);
```
                  
#### selecting distinct and not null: 
```
SELECT DISTINCT c1, c2 
  FROM tableName 
    WHERE c1 IS NOT NULL 
      ORDER BY c1, c2;
```

#### calculated fields
`SELECT salary/12 AS monthSalary`

`SELECT SUM(priceeach*quantityOrdered) AS total`

`WHERE amount > (SELECT AVG(amount) FROM payments)`

`WHERE rental_date + INTERVAL f.rental_duration DAY < CURRENT_DATE()`
> calculated date fields

`WHERE p.amount = (SELECT MAX(amount) FROM payment)`

`WHERE Rental = (SELECT MAX (COUNT (DISTINCT r.rental_id) Rental) FROM rental)`


## WHERE 
#### BETWEEN/ NOT BETWEEN
`WHERE salary BETWEEN 20000 AND 30000`
 > where salary >= 20000 and salary <= 30000
 
#### IN /NOT IN
`WHERE position IN('Manager', 'Supervisor')`
 > where position = 'Manager' OR 'Supervisor'

#### LIKE/ NOT LIKE
`LIKE 'H_ _ _'` = first letter H, there are 3 letters

`LIKE 'a%'`	= Finds any values that start with "a"

`LIKE '%a'`	= Finds any values that end with "a"

`LIKE '%or%'`	= Finds any values that have "or" in any position

`LIKE '_r%'`	= Finds any values that have "r" in the second position

`LIKE 'a_%'`	= Finds any values that start with "a" and are at least 2 characters in length

`LIKE 'a_ _%'`	= Finds any values that start with "a" and are at least 3 characters in length

`LIKE 'a%o'`	= Finds any values that start with "a" and ends with "o"

#### IS NULL/ IS NOT NULL
`WHERE c1 IS NOT NULL`

## ORDER BY
`ORDER BY column DESC / ASC`

`ORDER BY type, rent DESC` = order by type first then by rent in descending order

## COUNT
`COUNT(*)`

`COUNT(DISTINCT ...) AS myCount`

## GROUP BY & HAVING 
HAVING filters groups while WHERE filters individual columns
```
GROUP BY branchNO
   HAVING COUNT(StaffNo) > 2
```

## JOIN
(INNER) JOIN: Returns records that have matching values in both tables

LEFT (OUTER) JOIN: Returns all records from the left table, and the matched records from the right table

RIGHT (OUTER) JOIN: Returns all records from the right table, and the matched records from the left table

FULL (OUTER) JOIN: Returns all records when there is a match in either left or right table

#### INNER JOIN
join only rows with matching value: no NULL
```
INNER JOIN (SELECT CONCAT(first_name, ', ', last_name) AS actor, actor_id, film_id 
                FROM film_actor 
                     INNER JOIN actor USING (actor_id)) c 
         USING (film_id)
```

