# Laravel-PushBullet

This package is an integration of `joetannenbaum/phpushbullet` library in laravel 4.

## Table of Contents

+ [Installation](#installation)
+ [Listing Devices](#listing-devices)
+ [Pushing](#pushing)
  + [To Devices](#to-devices)
  + [To Type of evices](#to-type)
  + [To Users](#to-users)
+ [Types](#types)
  + [Notes](#notes)
  + [Links](#links)
  + [Addresses](#addresses)
  + [Lists](#lists)
  + [Files](#files)

## Installation


```
{
    "require": {
        "lahaxearnaud/laravel-pushbullet": "~0.1"
    }
}
```

Publish configurations

```
php artisan config:publish lahaxearnaud/laravel-pushbullet

```

Add provider in your `app.php`


```
'providers' => array(
    //...
    'Lahaxearnaud\LaravelPushbullet\LaravelPushbulletServiceProvider',
),

```

Add facade in your `app.php`


```
'aliases' => array(
    //...
    'PushBullet'        => 'Lahaxearnaud\LaravelPushbullet\LaravelPushbulletFacade',
),

```

Set the api key in `config/packages/lahaxearnaud/laravel-pushbullet/config.php`

```
  'apiKey' => 'MY-APPI-KEY'
```

If you do not wish to put your access token in your code (understandable), simply set it to the environment variable named `pushbullet.access_token` and set:

```
  'apiKey' => $_ENV['pushbullet.access_token']
```


## Listing Devices

To list the available devices on your account:

```php
PushBullet::devices();
```

This will return an array of objects with all of the device information.

## Pushing

### To Devices

When pushing a to a device, simply use the device's `nickname` or their `iden` from the list above.

To push to a single device:

```php
PushBullet::device('Chrome')->note('Remember', 'Buy some eggs.');
```

To push to multiple devices:

```php
PushBullet::device('Chrome')->device('Galaxy S4')->note('Remember', 'Buy some eggs.');
// or
PushBullet::device('Chrome', 'Galaxy S4')->note('Remember', 'Buy some eggs.');
```

If you want to push to all devices

```php
PushBullet::all()->note('Remember', 'Buy some eggs.');
```

### To Type

You can select a type of device (ex android)
```
PushBullet::type('android')->note('Remember', 'Buy some eggs.');
// or
PushBullet::type('android')->type('chrome')->note('Remember', 'Buy some eggs.');
// or
PushBullet::type('android', 'chrome')->note('Remember', 'Buy some eggs.');
```



### To Users

When pushing a to a user, simply use the user's email address:

To push to a single user:

```php
PushBullet::user('joe@example.com')->note('Remember', 'Buy some eggs.');
```

To push to multiple users:

```php
PushBullet::user('joe@example.com')->user('anne@example.com')->note('Remember', 'Buy some eggs.');
// or
PushBullet::user('joe@example.com', 'anne@example.com')->note('Remember', 'Buy some eggs.');
```
## Types

### Notes

Arguments:

+ Title
+ Body

```php
PushBullet::device('Chrome')->note('Musings', 'Why are fudgy brownies better than cakey brownies?');
```

### Links

Arguments:

+ Title
+ URL
+ Body (optional)

```php
PushBullet::device('Chrome')->link('Look It Up', 'http://google.com', 'I hear this is a good site for finding things.');
```

### Addresses

Arguments:
+ Name
+ Address

```php
PushBullet::device('Chrome')->address('The Hollywood Sign', '4059 Mt Lee Drive Hollywood, CA 90068');
```

Alternatively, you can pass in an associative array:

```php
$address = [
  'address' => '4059 Mt Lee Drive',
  'city'    => 'Hollywood',
  'state'   => 'CA',
  'zip'     => '90068',
];

PushBullet::device('Chrome')->address('The Hollywood Sign', $address);
```

### Lists

Arguments:
+ Title
+ Items (array)

```php
$items = [
  'Socks',
  'Pants',
  'Keys',
  'Wallet',
];

PushBullet::device('Chrome')->list('Do Not Forget', $items);
```

### Files

Arguments:
+ File Name
+ File URL (must be publicly available)
+ Body (optional)

```php
PushBullet::device('Chrome')->file('The Big Presentation', 'http://example.com/do-not-lose-this.pptx', 'Final version of slides.');
```
