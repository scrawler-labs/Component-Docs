# Getting Started

## Why use Scrawler Router?
- Fully automatic, you dont need to define single manual route.
- Support manual route defination for your edge use case.
- No configrations , works out of the box with any php project.
- Stable and well tested.
- Saves lot of time while building RESTful applications

## Installation
You can install Scrawler Router via Composer. If you don't have composer installed , you can download composer from [here](https://getcomposer.org/download/)

```sh
composer require scrawler/router
```

## Setup

Note 4.x release changes the way router handles request and response, if you still wanna continue using old way with symfony components goto [3.x branch](https://github.com/scrawler-labs/router/tree/3.x) 

```php
<?php

use Scrawler\Router\Router;

$dir = '/path/to/your/controllers';
$namespace = 'Namespace\of\your\controllers';

$router = new Router();
// Register your directory for automatic routing
$router->register($dir,$namespace);

/**
* you can now also enblae route caching by passing your own PSR 16 implementation
* $cache = new Psr\SimpleCache\CacheInterface();
* $router->enableCache($cache);
**/

// Fetch method and URI from somewhere
$httpMethod = $_SERVER['REQUEST_METHOD'];
$uri = $_SERVER['REQUEST_URI'];

// Strip query string (?foo=bar) and decode URI
if (false !== $pos = strpos($uri, '?')) {
    $uri = substr($uri, 0, $pos);
}
$uri = rawurldecode($uri);

//Dispatch route and get back the response
[$status,$handler,$args,$debug] = $router->dispatch($httpMethod,$uri);
switch ($status){
  case \Scrawler\Router\Router::NOT_FOUND:
    //handle 404 error
    // $debug contains extra debug info useful to check failure in automatic routing
    break;
  case \Scrawler\Router\Router::METHOD_NOT_ALLOWED:
    //handle 405 method not allowed
    break;
  case \Scrawler\Router\Router::FOUND:
    //call the handler
    $response = call_user_func($handler,...$args);
    // Send Response
    //echo $response
}

```
Done now whatever request occurs it will be automatically routed . You don't have define a single route
