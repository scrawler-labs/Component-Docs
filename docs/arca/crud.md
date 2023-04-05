# CRUD

## Create

Create a model using the database instance, once you save the model Arca will automatically create required columns and tables for you.

**Note: Use singular model name with small case letters, also don't use special characters**

```php
$user = $db->create('user');
$user->name = "John Doe";
$user->email = "john@example.com";
$user->age = 22;
$user->save();
```

## Read 

A single record is instance of `Scrawler\Arca\Model` and multiple records(collection) is instance of `Scrawler\Arca\Collection` 

```php

// Get single record using id
$id = 1;
$user = $db->get('user',$id);
print($user);

//Read single column of record
print($user->name);
print($user->age);

//convert /Scrawler/Arca/Model to array
$user->toArray();

// Get all records from a table
$users = $db->get('user');
foreach($users as $user){
  // Perform some actions ..
}
```

## Update

To update a model just retrieve the model , modify the fields and save the model, Arca will automatically update record for you 

```php

$user = $db->get('user',1);
$user->name = "Pranjal Pandey";
$user->save();

```

## Delete

To delete a model just call delete method on the model

```php

$user = $db->get('user',1);
$user->delete();

```

