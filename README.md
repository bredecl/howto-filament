# howto-filament

```bash
composer create-project laravel/laravel .
composer require filament/filament:"^3.0-stable" -W
php artisan filament:install --panels
```
ingresa el nombre del panel

[configura el .env]

```bash
composer require spatie/laravel-permission
php artisan vendor:publish --provider="Spatie\Permission\PermissionServiceProvider"
php artisan optimize:clear
php artisan migrate
```

```bash
composer require bezhansalleh/filament-shield
```
Add the Spatie\Permission\Traits\HasRoles trait to your User model(s):
```php

use Spatie\Permission\Traits\HasRoles;

class User extends Authenticatable
{
    use HasRoles;

    // ...
}
```

Publish the config file then setup your configuration:
```bash
php artisan vendor:publish --tag=filament-shield-config
```
Register the plugin for the Filament Panels you want
```php
public function panel(Panel $panel): Panel
{
    return $panel
        ->plugins([
            \BezhanSalleh\FilamentShield\FilamentShieldPlugin::make()
        ]);
}
```
Now run the following command to install shield:
```bash
php artisan shield:install
```
You can install the package via composer:
```bash
composer require 3x1io/filament-user
```
Publish Translation and config
```bash
php artisan vendor:publish --tag="filament-user-config"
php artisan vendor:publish --tag="filament-user-translations"
```
and now clear cache
```bash
php artisan optimize:clear
```
Publish Resource
you can publish the resource to your project

```bash
php artisan filament-user:publish
```
```bash
composer require rappasoft/laravel-authentication-log
composer require tapp/filament-authentication-log:"^3.0"
php artisan vendor:publish --provider="Rappasoft\LaravelAuthenticationLog\LaravelAuthenticationLogServiceProvider" --tag="authentication-log-migrations"
composer require torann/geoip
php artisan migrate
php artisan vendor:publish --provider="Rappasoft\LaravelAuthenticationLog\LaravelAuthenticationLogServiceProvider" --tag="authentication-log-views"
php artisan vendor:publish --provider="Rappasoft\LaravelAuthenticationLog\LaravelAuthenticationLogServiceProvider" --tag="authentication-log-config"
php artisan vendor:publish --tag="filament-authentication-log-translations"
php artisan vendor:publish --tag="filament-authentication-log-config"
```


#Using the Resource
Add this plugin to a panel on plugins() method. E.g. in `app/Providers/Filament/AdminPanelProvider.php`:
```php
use Tapp\FilamentAuthenticationLog\FilamentAuthenticationLogPlugin;

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->plugins([
            FilamentAuthenticationLogPlugin::make(),
            //...
        ]);
}
```
That's it! Now you can see the Authentication Log resource on left sidebar.




You must add the `AuthenticationLoggable` and `Notifiable` traits to the models you want to track.
```php
use Illuminate\Notifications\Notifiable;
use Rappasoft\LaravelAuthenticationLog\Traits\AuthenticationLoggable;
use Illuminate\Foundation\Auth\User as Authenticatable;
 
class User extends Authenticatable
{
    use Notifiable, AuthenticationLoggable;

    use HasRoles;
}
```

editar config/geoip.php:
  'cache_tags' => [],

## Erores:

This cache store does not support tagging.
editar `.env` cambiar CACHE_DRIVER a CACHE_DRIVER=Array
