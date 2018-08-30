# Laravel

## Installation

* Download composer
* Install composer
> composer create-project laravel/laravel _myapp_
* Add V-Hosts and hosts file entry (optionnal)

## Launch built in PHP server

> php artisan serve

## Artisan CLI (command line interface)

> php artisan list

> php artisan help _migrate_

Create a crud controller (plural)
> php artisan make:controller _TodosController_ --resource

Create model (singular)
> php artisan make:model _Todo -m_

Create migration
> php artisan make:migration _add_todos_to_db -table=todos_

Run migration
> php artisan migrate

Run tinker and interact with db
> php artisan tinker

## Eloquent ORM

Makes querying and working with db very easy

> Use App\Todo;<br>
> $todo = new Todo;<br>
> $todo->title = 'Some Todo';<br>
> $todo->save();<br>

## Compile SASS

* Install node modules
> install npm

* Modify ressources/assets/sass/_variables.scss

* Compile assets or watch assets to compile
> npm run dev

or

> npm run watch

## Add custom CSS

* Create **_custom.scss** in ressources/assets/sass

* Add **@import 'custom'** in ressources/assets/sass/app.scss;

* Compile assets
> npm run dev

or

> npm run 

## Migration

* Create model (**-m** to create migration)
> php artisan make:model _Post_ -m

* Add fields to table in database/migrations
```php 
$table->string('title'); 
```

* Complete migration 
> php artisan migrate

## Tinker (generate db data)

* Make sure .env and database.php are correctly configured

* Use tinker
> php artisan tinker

* Check data count
> App\ModelName::count()

* Initiate new class
> $modelName = new App\ModelName();

* Add data
> $modelName->title = "Titre";

* Save data
> $modelName->save();

## Show routes

> php artisan route:list

Generate routes for a controller in web.php
```php
Route::resource('posts', 'PostsController');
```