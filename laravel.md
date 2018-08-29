# Laravel

## Installation

* Download composer
* Install composer
> composer create-project laravel/laravel _myapp_
* Add V-Hosts and hosts file entry

## Artisan CLI (command line interface)

> php artisan list

> php artisan help _migrate_

Create controller (plural)
> php artisan make:controller _TodosController_

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

