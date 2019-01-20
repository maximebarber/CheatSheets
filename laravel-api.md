# Laravel API

## Video tutorial
Starts at 19:00
<iframe width="560" height="315" src="https://www.youtube.com/embed/4pc6cgisbKE" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## Steps
### Create Model
> php artisan make:model ModelName

### Create Controller
> php artisan make:controller ModelNamesController --resource

### Add to *routes/api.php*
```php
// List markets
Route::get('markets', 'MarketsController@index');

// List single market
Route::get('market/{id}', 'MarketsController@show');

// Create new Market
Route::post('market', 'MarketsController@store');

// Update
Route::put('market', 'MarketsController@store');

// Delete
Route::delete('market/{id}', 'MarketsController@destroy');
```

### Create Resource

> php artisan make:resource ModelName

### Add to *ModelNamesController*
Header
```php
use App\User;
use App\Http\Resources\User as UserResource;
```
View list of elements
```php
public function index()
{
    $users = User::paginate(15);

    return UserResource::collection($users);
}
```
View single element
```php
public function show($id)
{
    $user = User::findOrFail($id);

    return new UserResource($user);
}
```
Create or Update
```php
$user = $request->isMethod('put') ? User::findOrFail($request->id) : new User;

$this->validate($request,[
    'name' => 'required|string|max:50',
    'email' => 'required|string|email|max:255|unique:users',
    'password' => 'required|string|min:6|confirmed',
]);

$user->id = $request->input('id');
$user->name = $request->input('name');
$user->email = $request->input('email');
$user->password = Hash::make($request->input('password'));

if($user->save())
{
    return new UserResource($user);
}
```
Destroy
```php
public function destroy($id)
{
    $user = User::findOrFail($id);

    if($user->delete())
    {
        return new UserResource($user);
    }
}
```

### Delete data wrapping
Add to *app/Providers/AppServiceProvider.php*

```php
public function boot()
{
    Schema::defaultStringLength(191);

    // Resource without "data" wrapping
    Resource::withoutWrapping();
}
```

Don't forget to test in Postman ;)

