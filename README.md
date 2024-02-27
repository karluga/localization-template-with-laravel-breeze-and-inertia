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

# Notes
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
## Server setup
### Using Apache
1. Move all the code to server folder
2. Make an alias from "/" to "/public"

## Check out this guys repo
[Link to repo](https://github.com/MohmmedAshraf/laravel-translations)<br>
[Link to YouTube video](https://www.youtube.com/watch?v=FsgdjUK9b5Q&ab_channel=CodeWithTony)