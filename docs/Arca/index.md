# Getting Started

##  Why use Arca Orm ?
- Automatically creates tables and columns as you go
- No configuration, just fire and forget
- Save loads of time while working on database
- Built upon stable foundation of Doctrine Dbal and extensively tested
- Thanks to [loophp](https://github.com/loophp/collection) Arca comes with Lazy collection and tons of helper collection functions
- Supports lots database platforms , you can see the complete list [here](https://github.com/scrawler-labs/arca-orm/wiki/1.-Database-and-Drivers)
- Supports concurrent queries and connection pooling with swoole and async with amphp. Check out integration docs [here](https://github.com/scrawler-labs/arca-orm/wiki/7.-Using-with-Swoole-and-Amphp)


## Requirements
- PHP 8.1 or greater
- PHP PDO or other supported database adapter
- Mysql, MariaDB, Sqlite or any other supported database. check the list [here]([https://www.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/platforms.html#platforms](https://github.com/scrawler-labs/arca-orm/wiki/1.-Database-and-Drivers)) 


## Installation
You can install Arca ORM via Composer. If you don't have composer installed , you can download composer from [here](https://getcomposer.org/download/)

```
composer require scrawler/arca
```


## QuickStart

###  Setup
```php
   <?php
    include './vendor/autoload.php'
    
    $connectionParams = array(
        'dbname' => 'YOUR_DB_NAME',
        'user' => 'YOUR_DB_USER',
        'password' => 'YOUR_DB_PASSWORD',
        'host' => 'YOUR_DB_HOST',
        'driver' => 'pdo_mysql', //You can use other supported driver this is the most basic mysql driver
    );

    // For Arca ORM 1.x
    // $db =  new \Scrawler\Arca\Database($connectionParams);
    
    // For Arca 2.x and later 
    $db = \Scrawler\Arca\Facade\Database::connect($connectionParams);
    
```
For complete list of driver check [here](https://github.com/scrawler-labs/arca-orm/wiki/1.-Database-and-Drivers)

!!! info "ID and UUID"

    using uuid instead of id is a good idea but it may come with some performance issues, uuid even takes up more space than auto increment id. For your usecase if you want to use uuid as primary key instead on auto increment id just do the following 

    ```php
    $db->useUUID();
    ```
    once you have switched to UUID don't switch back to using id as it will cause lot of unwanted issues.


    
### CRUD
``` php

    // Create new record
    // The below code will automatically create user table and store the record

    $user = $db->create('user');
    $user->name = "Pranja Pandey";
    $user->age = 24
    $user->gender = "male"
    $user->save()
    
    // Get record with id 1
    
    $user = $db->get('user',1);
    
    //Get all records
    
    $users = $db->get('user');
    
    // Update a record
     $user = $db->get('user',1);
     $user->name = "Mr Pranjal";
     $user->save();
     
    // Delete a record
     $user = $db->get('user',1);
     $user->delete();

```

### Finding data with query
``` php

  // Using where clause
  $users = $db->find('user')
              ->where('name = "Pranjal Pandey"')
              ->get();
              
  foreach ($users as $user){
  // Some logic here 
  }
  
  // Get only single record
  $users = $db->find('user')
             ->where('name = "Pranjal Pandey"')
             ->first();  

  // Using limit in query
  $users = $db->find('user')
              ->setFirstResult(10)
              ->setMaxResults(20);
              ->get()

```
