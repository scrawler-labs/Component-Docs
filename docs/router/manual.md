# Manual Routing 

## How add manual route ?

Manual routes can be added to route collection, Router first tries to resolve manual routes then it falls back to automated routing. 
Manual routes always takes precedence over automated routes

```php
<?php
$collection = new RouteCollection($dir,$namespace)

// GET /hello
$collection->get('/hello',function(){
    return 'Hello World';
})

$router = new Router($collection);
$response = $router->dispatch();
$response->send();

```

## Functions for defining manual route
Manual routes can be defined by diffining endpoint on diffrent http methods

```php
<?php

$collection->get($route,$callable)
$collection->post($route,$callable)
$collection->put($route,$callable)
$collection->delete($route,$callable)

```

## Routing with pattern
You can also define `:numeric` , `:string` and `:alpha` as pattern in your routes

```php

$collection->get( "/",function(){
    return 'Hello'
});

$collection->get( "/page/:number",function($page){
    return 'Page number is :'.$page
});

$collection->get( "/product/:alpha",function($product){
    return 'Product is :'.$product
});

$collection->get( "/name/:string",function($name){
    return 'Name is :'.$name
});

```

## Routing with regex
You can also use regex patterns for your routes, above examples can also be written as

```php

$collection->get( "/",function(){
    return 'Hello'
});

$collection->get( "/page/([0-9]+)",function($page){
    return 'Page number is :'.$page
});

$collection->get( "/product/([a-zA-Z0-9-_]+)",function($product){
    return 'Product is :'.$product
});

$collection->get( "/name/([a-zA-Z]+)",function($name){
    return 'Name is :'.$name
});

```