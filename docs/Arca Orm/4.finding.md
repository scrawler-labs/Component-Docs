# Finding (Query)

## Finding
Thanks to Doctrine DBAL Arca comes with a powerful query builder, to get instance of query builder just use the `find()` function. Once you have built the query just user `get()` to execute query and get multiple records or `first()` to execute query and get single record.  

```php

// Get multiple records (returns \Scrawler\Arca\Collection)
$users = $db->find('user')
            ->where('name = "Pranjal Pandey"')
            ->get();

// Get single record (returns \Scrawler\Arca\MOdel)
$users = $db->find('user')
            ->where('name = "Pranjal Pandey"')
            ->first();
``` 

## WHERE-Clause

Arca supports where query using `where()` function and to use multiple where query just add `andWhere()` or `orWhere()`

```php

// AND Where
$users = $db->find('user')
            ->where('name = "Pranjal Pandey"')
            ->andwhere('age = 22')
            ->get();

// OR Where
$users = $db->find('user')
            ->where('name = "Pranjal Pandey"')
            ->orwhere('name = "John Doe"')
            ->get();

```

## ORDER BY Clause
The `orderBy($sort, $order = null)` method adds an expression to the ORDER BY clause. 
_Note: Be aware that the optional $order parameter is not safe for user input and accepts SQL expressions._

```php

$users = $db->find('user')
            ->orderBy('username', 'ASC')
            ->addOrderBy('last_login', 'ASC NULLS FIRST')
            ->get();

```

## LIMIT Clause
Arca supports LIMIT clause on all vendor using `setFirstResult($offset)` to set the offset and `setMaxResults($limit)` to set the limit of results returned.

```php

$users = $db->find('user')
           ->setFirstResult(10)
           ->setMaxResults(20)
           ->get();

```

## GROUP BY Clause

Arca supports GROUP BY query using `groupBy()` to have multiple group by you can use `addGroupBy()`

```php
$users = $db->find('user')
            ->groupBy('last_login')
            ->get();
```

