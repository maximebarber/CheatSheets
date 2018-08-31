# Laravel

## Table of contents
1. [Installation](#1-installation)
2. [Launch built in PHP server](#2-launch-built-in-php-server)
3. [Artisan CLI](#3-artisan-cli)
4. [Eloquent ORM](#4-eloquent-orm)
5. [Compile SASS](#5-compile-sass)
6. [Add custom CSS](#6-add-custom-css)
7. [Migration](#7-migration)
8. [Tinker](#8-tinker)
9. [Show routes](#9-show-routes)
10. [Create Form w/ Laravel Collective](#10-create-form-w-laravel-collective)
11. [Create input text editor w/ CKEditor Package](#11-create-input-text-editor-w-ckeditor-package)
12. [User Authentication](#12-user-authentication)
13. [Model relationships](#13-model-relationships)
14. [Access control](#14-access-control)

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

## 4. Eloquent ORM

Makes querying and working with db very easy

> Use App\Todo;<br>
> $todo = new Todo;<br>
> $todo->title = 'Some Todo';<br>
> $todo->save();<br>

## 5. Compile SASS

* Install node modules
> install npm

* Modify ressources/assets/sass/_variables.scss

* Compile assets or watch assets to compile
> npm run dev

or

> npm run watch

## 6. Add custom CSS

* Create **_custom.scss** in ressources/assets/sass

* Add **@import 'custom'** in ressources/assets/sass/app.scss;

* Compile assets
> npm run dev

or

> npm run 

## 7. Migration

* Create model (**-m** to create migration)
> php artisan make:model _Post_ -m

* Add fields to table in database/migrations
```php 
$table->string('title'); 
```

* Complete migration 
> php artisan migrate

### Add field to table

> php artisan make:migration _add_user_id_to_posts_

* Update field
```php
public function up()
{
    $upField = function ($table) 
    {
        $table->integer('user_id');
    };

    Schema::table('posts', $upField);
}
```

* Delete field
```php
public function down()
{
    $downField = function ($table) {
        $table->dropColumn('user_id');
    };

    Schema::table('posts', $addField);
}
```

* Complete migration 
> php artisan migrate

## 8. Tinker

Generate db data

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

## 9. Show routes

> php artisan route:list

Generate routes for a controller in web.php
```php
Route::resource('posts', 'PostsController');
```

## 10. Create Form w/ Laravel Collective

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
## 11. Create input text editor w/ CKEditor Package

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

## 12. User Authentication

> php artisan make:auth / yes

## 13. Model relationships

Post.php
```php
public function user()
{
    return $this->belongsTo('App\User')
}
```

User.php
```php
public function posts()
{
    return $this->hasMany('App\Post');
}
```

Get data w/ blade
```php
{{ $post->user->name }}
```

## 14. Access control

Controller
```php
/**
 * Create a new controller instance.
 *
 * @return void
 */
public function __construct()
{
    $this->middleware('auth', ['except' => ['index', 'show']]);
}
```

Manage display in view
```php
@if(!Auth::guest())
    <p>Do not display to guests</p>
@endif
```