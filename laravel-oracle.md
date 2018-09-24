# Laravel-Oracle
https://github.com/yajra/laravel-oci8

## Server Requirements

* PHP >= 5.6.4
* OCI8 PHP Extension

### Install OCI8 PHP Extension

For MAC
* http://techblog.ankitaoza.com/2017/04/07/installing-php-oci8-extension-on-mac-osx10-11-6/
* https://antistatique.net/fr/nous/bloggons/2013/03/25/install-php-oracle-oci-extension-11-2-on-mac-os-x-10-8

## Install Laravel OCI8

Get Laravel version
> php artisan laravel -V

Quick installation
> composer require yajra/laravel-oci8:"{laravel.version}"

Service Provider (config/app.php)
```
Yajra\Oci8\Oci8ServiceProvider::class,
```

Create configuration file (config/oracle.php)
> php artisan vendor:publish --tag=oracle

Configure .env
```php
'driver'         => 'oracle',
'tns'            => '(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST={host})(PORT={port}))(CONNECT_DATA=(SERVICE_NAME={sid})))',
//'host'           => env('DB_HOST', ''),
//'port'           => env('DB_PORT', '1521'),
'database'       => '{database-name}',
'username'       => '{username}',
'password'       => '{password}',
```

## Get Data

### Create model
> php artisan make:model {TableName}

```php
namespace App;

use Yajra\Oci8\Eloquent\OracleEloquent as Eloquent;

class {ClassName} extends Eloquent{}
```

### Create controller and test
> php artisan make:controller {TableName}Controller --resource

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\{ModelName};
use DB;

class {ControllerName} extends Controller
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        $tests = DB::select('select * from {TableName}');
        return view('{TableName}.index')->with('tests', $tests);
    }
```

### Create blade view

```php
@foreach($tests as $test)
    {{ $tests->field_name }}
@endforeach
```

## Useful links

* http://broncodev.com/2017-06-18-laravel5-oracle/
* https://laracasts.com/discuss/channels/guides/fresh-install-of-macos-high-sierra-131-with-laravel-valet-php-and-oracle-oci8
* https://yajrabox.com/docs/laravel-oci8/master/installation