# Getting Started

## Why use Scrawler Router?
- Fully automatic, you dont need to define single manual route.
- No configrations , works out of the box with any php project.
- Stable and used internally within many [Corpuvision](https://corpusvision.com)'s projects
- Saves lot of time while building RESTful applications

## Installation
You can install Scrawler Router via Composer. If you don't have composer installed , you can download composer from [here](https://getcomposer.org/download/)

```sh
composer require scrawler/router
```

## Setup

```php
<?php

use Scrawler\Router\RouteCollection;
use Scrawler\Router\Router;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\HttpFoundation\Request;


$dir = /path/to/your/controllers;
$namespace = Namespace\of\your\controllers;

$collection = new RouteCollection($dir,$namespace)

/**
* As of v3.2.0 you can now enblae route caching and optionally pass your own PSR 16 implementation
* $collection = new RouteCollection($dir,$namespace,true);
* OR with your own cache adapter
* $cache = new Psr\SimpleCache\CacheInterface(); 
* $collection = new RouteCollection($dir,$namespace,true,$cache);
**/

$router = new Router($collection);
//Optional you can now pass your own Request object to Router for Router to work on
//$router = new Router($collection,Request $request);


//Dispatch route and get back the response
$response = $router->dispatch();
// Or Alternatively you can pass header as optional argument
//$response = $router->dispatch(['content-type' => 'application/json']);


//Do anything with your Response object here
//Probably middleware can hook in here

//send response
$response->send();
```
