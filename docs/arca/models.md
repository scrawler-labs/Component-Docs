# Models and Collection

## Model

A row in database is represented by a model in Arca. Arca can perform all magic due to models to create a new row, you just need to create a new model and save 

```php
//create a new model 
$user = $db->create('user');
$user->name = "John Doe";
$user->email = "John@test.com";

//Save functions returns the id of newly created/ updated record
$id = $user->save();

```

### Magic methods
Model utilised php's magic __get() and __set() method to provide a neat and simple ways to set values in model and retrive values , once a row is fetched it is sync with model properties

### Helper functions
Model comes with few helper to make your life easier

```php
$user = $db->get('user',1);

// Converts model object to an array with properties
$user->toArray();

// Converts model object to json string
$user->toString();

//unset a value
unset($user->name)

// returns the name of associated table
$user->getName();

//Bulk set properties using array
$array = ['name'=>'Pranjal','email'=>'itspranjalpandey@gmail.com']
$user->setProperties($array);
$user->save();

// Check if property exist exists
isset($user);

```

## Collection
A collection represent multiple rows of database if a query returns multiple rows. A `collection class` is a collection of Models. Collection comes with multiple helper utility. 

```php

$users = $db->get('user');

// You can iterate through collection like regular arrays
foreach($users as $user){
  //Note: $user will be a instance of \Scrawler\Arca\Model
  print($user->name);
}

// You can convert collection to array 
$users->toArray()

// You can convert collection to json string 
$users->toString();
```
!!! info 

    To learn more visit [Collections doc](collections.md)

