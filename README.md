# Laravel Convenient System notifications

[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)
[![Laravel Version](https://img.shields.io/badge/laravel-5-orange.svg?style=flat-square)](http://laravel.com)

Notification system for Laravel 5.

Often after saving some data from user you have to redirect to proper page and notificate user that everything done successfully or some errors appeared.

Now you can do this more convenient and easy way.

## Install

Add

``` JSON
"gaaarfild/laravel-notifications": "dev-master"
```

to your `composer.json` file into `require` section.

Then type in console

``` BASH
$ composer update
```

When update completed, add to your `config/app.conf` file to `providers` section

``` PHP
'providers' => [
    // ...
    Gaaarfild\LaravelNotifications\LaravelNotificationsServiceProvider::class,
]
```

If you want to use `Notifications` facade, add to same file at the `aliases` section

``` PHP
'aliases' => [
    // ...
  'Notifications' => Gaaarfild\LaravelNotifications\NotificationsFacade::class,
]
```

## Usage

### Save messages for the next request

``` php
Notifications::add('Your message text', 'type', 'group');
```

`$type` param used especially for Twitter Bootstrap render. It displays alerts with respective class.

i.e. If you set `type` to `danger`, alert with class 'alert alert-danger' will be generated on `toBootstrap()` formate method.

`$group` param groups messages to groups. :) On the next Request you can retrieve them by group.


### Retrieving messages

#### All messages

``` PHP
Notifications::all()->get();
```

#### Messages by group

``` PHP
Notifications::byGroup('group')->get();
```

#### Messages by type

``` PHP
Notifications::byType('type')->get();
```

### Format messages

You also can format messages

#### JSON

You can retrieve and format all messages as JSON

``` PHP
Notifications::all()->toJson();
```

Or can filter them by group or type

``` PHP
Notifications::byType('success')->toJson();

Notifications::byGroup('login')->toJson();
```


#### Twitter Bootstrap Alerts

You can also format your messages directly to Twitter Bootstrap alerts.

``` PHP
Notifications::all()->toBootstrap();
```

And you can filter them by group or type as well:


``` PHP
Notifications::byType('success')->toBootstrap();

Notifications::byGroup('login')->toBootstrap();
```

[Twitter Bootstrap](http://getbootstrap.com) required.

### Other

#### Count Messages

``` PHP
Notifications::all()->count();
```

#### Get First Message

``` PHP
Notifications::all()->first();
```

#### FormRequest usage

You can also override form request method `formatErrors()`, to display errors from validator in your Form Requests.

``` PHP

    public function formatErrors(Validator $validator){
        foreach ($validator->errors()->all() as $error) {
            Notifications::add($error, 'danger');
        }

        return $validator->errors()->getMessages();
    }
    
```

## Contributions

Contributions are highly appreciated.

Send your pull requests to `master` branch.


## License

The MIT License (MIT). Please see [License File](https://github.com/gaaarfild/laravel-notifications/blob/master/LICENSE) for more information.

