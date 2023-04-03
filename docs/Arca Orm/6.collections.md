# Collections

## Collection
`\Scrawler\Arca\Collection` is based on [loophp-collection](https://github.com/loophp/collection) hence table row is lazily converted to model when required giving a performance boost.

## Helper functions
Here is some of the helper function Arca Collection provide.

```php
$users = $db->find('user')->where('active = 1')->get();
$adults = $db->find('user')->where('age > 18')->get();


//Get first element from collection
$users->first(); 

//Get last element from collection

// Merge two collections
$users->merge($adults);

//Map Data
$collection
    ->map(
        static function ($user, $key): string {
            //Note : $value will be instance of \Scrawler\Arca\Model
            unset($user->dob);
        }
    )
    ->all();

// Filter
$users 
    ->filter(static fn ($user): bool => $user->email != null);
// This filter removes all user with no email id

// Apply callback on every model
$users->apply(
        static function ($value, $key): bool {
            print($user->name);

            return true;
        }
    );

//limit collection to certain number of values
$users->limit(3);


```
!!! info "Standalone Collections"

    If you want to to create standalone collections  you can directly create instance of `loophp\collection\Collection` find all available methods [here](https://loophp-collection.readthedocs.io/en/stable/pages/usage.html#advanced)