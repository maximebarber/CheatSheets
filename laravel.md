# Laravel

## Table of contents
1. [Installation](#1.-installation)
2. [Launch built in PHP server](#2.-launch-built-in-php-server)
3.

## 1. Installation

* Download composer
* Install composer
> composer create-project laravel/laravel _myapp_
* Add V-Hosts and hosts file entry (optionnal)

## 2. Launch built in PHP server

> php artisan serve

## 3. Artisan CLI

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

## Create Form w/ Laravel Collective

### Installation

[Laravel Collective Installation](https://laravelcollective.com/docs/master/html)

### Controller

```php
public function create()
{
    return view('posts.create');
}
```

```php
public function store(Request $request)
{
    $this->validate($request, [
        'title' => 'required',
        'body' => 'required',
    ]);

    //Create Post
    $post = new Post;
    $post->title = $request->input('title');
    $post->body = $request->input('body');
    $post->save();

    return redirect('/posts')->with('success', 'Post created');
}
```

### View

```php
{!! Form::open(['action' => 'PostsController@store', 'method' => 'POST']) !!}

    <div class="form-group">

        {{ Form::label('title', 'Title') }}
        {{ Form::text('title', '', ['class' => 'form-control', 'placeholder' => 'Title']) }}

    </div>

    <div class="form-group">

        {{ Form::label('body', 'Body') }}
        {{ Form::textarea('body', '', ['class' => 'form-control', 'placeholder' => 'Body Text']) }}

    </div>

    {{ Form::submit('submit', ['class' => 'btn btn-outline-primary']) }}

{!! Form::close() !!}
```

### Display success/error messages

ressources/views/inc/messages.blade.php

```php
{{-- Display error message --}}
@if(count($errors) > 0)
    @foreach($errors->all() as $error)
        <div class="alert alert-danger">
            {{ $error }}
        </div>
    @endforeach
@endif

{{-- Display session success message --}}
@if(session('success'))
    <div class="alert alert-success">
        {{ session('success') }}
    </div>
@endif

{{-- Display session error message --}}
@if(session('error'))
    <div class="alert alert-danger">
        {{ session('error') }}
    </div>
@endif
```
ressources/views/inc/app.blade.php

```php
<div class="container">
    {{-- Success and error messages --}}
    @include('inc.messages')
    @yield('content')
</div>
```
## Create input text editor w/ CKEditor Package

### Installation

[CKEditor Installation](https://github.com/UniSharp/laravel-ckeditor)

### Apply

create.blade.php

```php
{{ Form::textarea('body', '', ['id' => 'article-ckeditor','class' => 'form-control', 'placeholder' => 'Body Text']) }}
```

### Modify blade

show.blade.php

```php
{!! $post->body !!}
```

## User Authetication