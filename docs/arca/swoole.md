# Using with Swoole and AmpPHP
If you are interested in using Arca ORM with Async libraries there are various drivers available for same. Here are example for usage

## Swoole
Scrawler Labs provide a integration for swoole Postgres [here](https://github.com/scrawler-labs/swoole-postgresql-doctrine)

### Installation 

```
composer require scrawler/swoole-postgresql-doctrine
``` 

### Usage with Arca ORM
Use the following configuration during setup 

```php
 <?php
    include './vendor/autoload.php'
    
    $connectionParams = array(
    'dbname' => 'YOUR_DB_NAME',
    'user' => 'YOUR_DB_USER',
    'password' => 'YOUR_DB_PASSWORD',
    'host' => 'YOUR_DB_HOST',
    'driverClass' =>\Scrawler\Swoole\PostgreSQL\Driver::class,
    'poolSize' => 8, //you can set pool size to any number of parallel connection your db can support
    );

    $db =  new \Scrawler\Arca\Database($connectionParams);

```

To know about using Co-routines please check readme [here](https://github.com/scrawler-labs/swoole-postgresql-doctrine)

## Amphp
You can use amphp with ARCA ORM using there official [mysql-dbal](https://github.com/amphp/mysql-dbal) implementation 

### Installation 

```
composer require amphp/mysql-dbal
``` 

### Usage with Arca ORM
Use the following configuration during setup 

```php
 <?php
    include './vendor/autoload.php'
    
    $connectionParams = array(
    'driverClass' => \Amp\Mysql\DBAL\MysqlDriver::class,
    'user' => 'YOUR_DB_USER',
    'password' => 'YOUR_DB_PASSWORD',
    'dbname' => 'YOUR_DB_NAME',
    'host' => 'YOUR_DB_HOST'
    );

    $db =  new \Scrawler\Arca\Database($connectionParams);
```
