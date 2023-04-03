#  Redirection
If you want to redirect a request you can return a Symphony redirect response

```php
 use Symfony\Component\HttpFoundation\RedirectResponse;
 use Symfony\Component\HttpFoundation\Session\Session;

 // Inside hello.php
class Hello
{

// set flash messages
    
    public function getAbc()
    {
      // redirect to external urls
      return new RedirectResponse('http://example.com/');

     // Or alternatively you can set your arguments in flashbagk and redirect to internal URL 
     // Note you may use any flash manager to achieve this but as HttpFoundation is already a dependecy of Router here is a exmple with Symfony Session
     $session = new Session();
     $session->start();   
     $session->getFlashBag()->add('notice', 'Profile updated');
     return new RedirectResponse('http://mydomain.com/profile');
    
    }
}
```
Infact from Scrawler Router 3.1.0 you can directly return object of [\Symfony\Component\HttpFoundation\Response](https://symfony.com/doc/current/components/http_foundation.html#response) from your controller
