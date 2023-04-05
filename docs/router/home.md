# Website homepage
Scrawler Router uses a special function name `allIndex()` and special controller name `Main`. So If you want to make a controller for your landing page `\` the controller will be defines as follows
```php
// Inside main.php
class Main
{
    // All request to your landing page will be resolved to this controller
    // ALternatively you can use getIndex() to resolve only get request
    public function allIndex()
    {
    }
}
```

## Main Controller
Class name with `Main` signifies special meaning in Scrawler Router , if you wanna define pages route URL you can use main controler
```php
// Inside main.php
class Main
{
    // Resolves `/`
    public function getIndex()
    {
    }
    
    // Resolves `/abc`
    public function getAbc()
    {
    
    }
    
    // Resolves `/hello`
    public function getHello()
    {
    
    }
}
```

## Index function
Just like `Main` controller `allIndex(), getIndex(), postIndex()` etc signifies a special meaning , urls with only controller name and no function name will try to resolve into this function.
```php
// Inside hello.php
class Hello
{
    // Resolves `/hello`
    public function getIndex()
    {
    
    }
    
    // Resolves `/hello/abc`
    public function getAbc()
    {
    
    }
}
```
