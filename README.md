# Project template using laravel breeze UI with localization

## Local setup (these steps were not tested, this is just a guide)

1. Clone this repo
2. Install dependencies
```
composer install (est. 2-5min)
npm install (est. 2min)
```
3. Add database credentials to `.env` file.
4. Migrations 
```
php artisan migrate
```
5. Generate application encryption key using `php artisan key:generate`.
6. Launch locally using `php artisan serve`
7. To be able to access the routes at  http://localhost:8000 you need to run `npm run dev`

## Notes
### NOTE 1
Theres a problem in the `C:\wamp64\www\localization-template-with-laravel-breeze-and-inertia\vendor\stichoza\google-translate-php\src\GoogleTranslate.php` file because CURLOPT_SSL_VERIFYPEER is not false
```
public function __construct(string $target = 'en', string $source = null, array $options = [], TokenProviderInterface $tokenProvider = null, bool|string $preserveParameters = false)
{
    $this->client = new Client([
        'verify' => false, // Disable SSL verification for testing (remove this in production)
    ]);

    $this->setTokenProvider($tokenProvider ?? new GoogleTokenGenerator)
        ->setOptions($options) // Options are already set in client constructor though.
        ->setSource($source)
        ->setTarget($target)
        ->preserveParameters($preserveParameters);
}
```
### NOTE 2
In the Inertia.js package there was a really bad problem where the app URL gets duplicated 
File: `vendor\inertiajs\inertia-laravel\src\Response.php`
Temporary solution:
```
$page = [
    'component' => $this->component,
    'props' => $props,
    'url' => $request->fullUrl(),
    'version' => $this->version,
];

// Add this method inside the class
public function fullUrl()
{
    $query = $this->getQueryString();

    $question = $this->getBaseUrl().$this->getPathInfo() === '/' ? '/?' : '?';

    return $query ? $this->url().$question.$query : $this->url();
}
```
Credit:
[GitHub link](https://github.com/inertiajs/inertia-laravel/pull/360)
### NOTE 3
Inside `routes/web.php` file add this line at the end to make the routes actually work:
```
Route::get('/{any}', function () { return view('app'); })->where('any', '.*');
```

## Server setup
### Using Apache
1. Move all the code to server folder
2. Make an alias from "/" to "/public"

## Check out this guys repo
[Link to repo](https://github.com/MohmmedAshraf/laravel-translations)<br>
[Link to YouTube video](https://www.youtube.com/watch?v=FsgdjUK9b5Q&ab_channel=CodeWithTony)