# Manual Routing 

## How add manual route ?

Manual routes can be added to route collection, Router first tries to resolve manual routes then it falls back to automated routing. 
Manual routes always takes precedence over automated routes

```php
<?php
// Initialize Router 
//$router = new Router();
//$router->register($dir,$namespace);

// GET /hello
$router->get('/hello',function(){
    return 'Hello World';
})

//Handle the response
//[$status,$handler,$args,$debug] = $router->dispatch($httpMethod,$uri);


```

## Functions for defining manual route
Manual routes can be defined by diffining endpoint on diffrent http methods

```php
<?php

$router->get($route,$callable)
$router->post($route,$callable)
$router->put($route,$callable)
$router->delete($route,$callable)

```

## Routing with pattern
You can also define `:numeric` , `:string` and `:alpha` as pattern in your routes

```php

$router->get( "/",function(){
    return 'Hello'
});

$router->get( "/page/:number",function($page){
    return 'Page number is :'.$page
});

$router->get( "/product/:alpha",function($product){
    return 'Product is :'.$product
});

$router->get( "/name/:string",function($name){
    return 'Name is :'.$name
});

```

## Routing with regex
You can also use regex patterns for your routes, above examples can also be written as

```php

$router->get( "/",function(){
    return 'Hello'
});

$router->get( "/page/([0-9]+)",function($page){
    return 'Page number is :'.$page
});

$router->get( "/product/([a-zA-Z0-9-_]+)",function($product){
    return 'Product is :'.$product
});

$router->get( "/name/([a-zA-Z]+)",function($name){
    return 'Name is :'.$name
});

```
