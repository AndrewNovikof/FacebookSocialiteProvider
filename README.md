# Facebook OAuth2 Provider for Laravel Socialite

[![Latest Stable Version](https://poser.pugx.org/andrewnovikof/facebookserviceprovider/v/stable)](https://packagist.org/packages/andrewnovikof/facebookserviceprovider)
[![Total Downloads](https://poser.pugx.org/andrewnovikof/facebookserviceprovider/downloads)](https://packagist.org/packages/andrewnovikof/facebookserviceprovider)
[![Latest Unstable Version](https://poser.pugx.org/andrewnovikof/facebookserviceprovider/v/unstable)](https://packagist.org/packages/andrewnovikof/facebookserviceprovider)
[![License](https://poser.pugx.org/andrewnovikof/facebookserviceprovider/license)](https://packagist.org/packages/andrewnovikof/facebookserviceprovider)

### 1. Installation

`composer require andrewnovikof/facebookserviceprovider`

### 2. Service Provider

* Remove `Laravel\Socialite\SocialiteServiceProvider` from your `providers[]` array in `config\app.php` if you have added it already.
* Add `SocialiteProviders\Manager\ServiceProvider` to your `providers[]` array in `config\app.php`.

For example:
```php
'providers' => [
    // a whole bunch of providers
    // remove 'Laravel\Socialite\SocialiteServiceProvider',
    SocialiteProviders\Manager\ServiceProvider::class, // add
];
```
* Note: If you would like to use the Socialite Facade, you need to [install it](http://laravel.com/docs/5.2/authentication#social-authentication).

### 3. Add the Event and Listeners

* Add `SocialiteProviders\Manager\SocialiteWasCalled::class` event to your `listen[]` array in `<app_name>/Providers/EventServiceProvider`.

* Add your listeners (i.e. the ones from the providers) to the `SocialiteProviders\Manager\SocialiteWasCalled[]` that you just created.

* The listener that you add for this provider is `AndrewNovikof\SocialiteProviders\Facebook\FacebookExtendSocialite::class`.

* Note: You do not need to add anything for the built-in socialite providers unless you override them with your own providers.

For example:
```php
/**
 * The event handler mappings for the application.
 *
 * @var array
 */
protected $listen = [
    SocialiteProviders\Manager\SocialiteWasCalled::class => [
        AndrewNovikof\SocialiteProviders\Facebook\FacebookExtendSocialite::class
    ],
];
```

### 4. Services Array and .env

Add to `config/services.php`:
```php
'facebook' => [
    'client_id' => env('FACEBOOK_ID'),
    'client_secret' => env('FACEBOOK_SECRET'),
    'redirect' => env('FACEBOOK_REDIRECT'),  
],
```

Append provider values to your `.env` file:
**Note: Add both public and secret keys!**
```
// other values above
FACEBOOK_ID=your_app_id_for_the_service
FACEBOOK_SECRET=your_app_public_for_the_service
FACEBOOK_REDIRECT=https://example.com/login
```
