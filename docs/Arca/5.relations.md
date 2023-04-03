# Relations
Arca takes heavy lifting of relations from you and provide a simple and clean way to work with relations using simple NoSQL like approach 

## one-to-one

To save two tables with one-to-one relation just pass child model to parent model with key as child `$parent->child = $child` Arca will save both tables for you and create a one-to-one relation amongst them too.

```php

//Saving record
$engine = $db->create('engine');
$engine->name = 'straight six engine';
$engine->manufacturer = 'BMW';

$car = $db->create('car')
$car->name = 'BMW M340i';
$car->engine = $engine
$car->save();

// Retrieving one-to-one relation 
$car = $db->get('car',1);
print($car->engine);

```

## one-to-many
To save two tables with one-to-many relation just pass multiple children models to parent model with key as "selfChildList"
`$parent->selfChildList = [$child_one,$child_two]` Arca will save all records for you and create a one-to-many relation amongst them, to do this Arca adds a key `parent_id` to the child table

```php

//Saving record
$burger = $db->create('food');
$burger->name = 'burger';
$burger->price = 100;

$pizza = $db->create('food');
$pizza->name = 'pizza';
$pizza->price = 220;

$restaurant = $db->create('restaurant');
$restaurant->name = 'Food Joint';
$restaurant->selfFoodList = [$burger,$pizza];
$restaurant->save(); // restaurant_id will be added as foreign key to food table

// Retrieving one-to-many relation;
$restaurant = $db->get('restaurant',1);
$foods = $restaurant->selfFoodList;
foreach($foods as $food){
print($food);
}

// You can even retrieve parent table from child table;
$food = $db->get('food',1);
print($food->restaurant);  

```

## many-to-one
This works just as inverse on one-to-many, to create a many-to-one relation just store the parent key to all child models `$child->parent = $parent`

```php

$shop= $db->create('shop');
$shop->name = 'Toy Shop';
$shop->save();

//Important : parent needs to be saved first before being refrenced in child
$car= $db->create('toy');
$car->name = 'RC Car';
$car->price = 320;
$car->shop = $shop;
$car->save();

$barbie = $db->create('toy');
$barbie->name = 'Barbie';
$barbie->price = 550;
$barbie->shop = $shop;
$barbie->save();


// Retrieving parent from child
$toy = $db->get('toy',1);
print($toy->shop);

//retriving column of parent
print($toy->shop->name);  

```

## many-to-many
To save two tables with many-to-many relation just pass multiple children models to parent model with key as "sharedChildList"
`$parent->sharedChildList = [$child_one,$child_two]`. Arca will shave all models and create a relational table named `parent_child`
unlike one-to-many in many-to-many both table can have list of other table inversely

```php

//Saving record
$burger = $db->create('food');
$burger->name = 'burger';
$burger->price = 100;
$burger->save();

$pizza = $db->create('food');
$pizza->name = 'pizza';
$pizza->price = 220;
$pizza->save();

$restaurant = $db->create('restaurant');
$restaurant->name = 'Food Joint';
$restaurant->sharedFoodList = [$burger,$pizza];
$restaurant->save(); // restaurant_id will be added as foreign key to food table

$restaurant_two = $db->create('restaurant');
$restaurant_two->name = 'Snack Junkie';
$restaurant_two->sharedFoodList = [$burger,$pizza];
$restaurant_two->save();
// Retrieving one-to-many relation;
$restaurant = $db->get('restaurant',1);
$foods = $restaurant->sharedFoodList;
foreach($foods as $food){
print($food);
}


// inversely yo can get list of restaurant from food;
$food = $db->get('food',1);
$restaurants = $food->sharedRestaurantList ;
foreach($restaurants as $restaurant){
print($restaurant);
}


```