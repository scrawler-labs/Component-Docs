# Automatic Routing 

## How it Works ?

The automatic routing is possible by following some conventions. Lets take a example lets say a controller Hello

```php
<?php
//Hello.php

class Hello
{
    public function getWorld()
    {
        return "Hello World";
    }
}
```
Now calling `localhost/hello/world` from your browser you will see `hello world` on your screen.


##  How is it able to do it automatically ?

Each request to the server is interpreted by Scrawler Router in following way:

```shell
METHOD    /controller/function/arguments1/arguments2 
```

The controller and function that would be invoked will be

```php
<?php

class Controller
{
    public function methodFunction($arguments1, $arguments2)
    {
        //Definition goes here
    }
}
```
For Example the following call:

```shell
GET  /user/find/1
```

would invoke following controller and method

```php
<?php

class User
{
    public function getFind($id)
    {
        //Function definition goes here
    }
}
```
!!! Info
    In above example `1` will be passed as argument `$id`

## How should I name my function for automatic routing?

The function name in the controller should be named according to following convention
```shell
methodFunction
```
!!! Note
    The method should always be written in small and the first word of function name should always start with capital.


Valid methods are:
```shell
all - maps any kind of request method i.e it can be get,post etc
get - mpas url called by GET method
post - maps url called by POST method
put - maps url called by PUT method
delete - maps url called by DELETE method
```
Some eg. of <b>valid</b> function names are:
```shell
getArticles, postUser, putResource
```
<b>Invalid</b> function names are:
```shell
GETarticles, Postuser, PutResource
```
