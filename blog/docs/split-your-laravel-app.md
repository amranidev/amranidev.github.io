# Split your laravel app

Sometimes you work on a laravel app project, the app get much bigger by time, especially when it contains a lot of dependencies between modules, and you remind that each module might be splitted or you deserve to make an app for each module, the last one is not a good way because we stuck in redundancy.

It's difficult to maintain all your bussiness logic behind the scence.

Thats why your app deserve to be splitted into packages/modules.

So you can split modules by creating packages into your app by yourselves, or 
it recomended to use one of these packages.

 * [Lpackager](https://github.com/amranidev/lpackager) 
 * [modules](https://github.com/caffeinated/modules)
 * [laravel-packager](https://github.com/Jeroen-G/laravel-packager)

### Implementation

In this example we're going to use [Lpackager](https://github.com/amranidev/lpackager).

Lpackager propose a way to generate your modules/packages simply without forgeting MVC laravel structure via an artisan command.

`php artisan lpackager:package <PackageName> <Path> <"NameSpace">`

#### File Structure
```
 PackageName
 |
 |__config
 |  |__config.php
 |
 |__database
 |  |__migrations 
 |
 |__resources
 |  |__views
 |     |__welcome.blade.php
 |
 |__src
 |  |__Http
 |  |  |__Controllers
 |  |  |  |__WelcomeController.php
 |  |  |__routes.php
 |  |__ServiceProvider.php				
 |
```
After **Lpackager** installation, lets create our first package via an artisan command : 

`php artisan lpackager:package Client kernel "Kernel\Client"`

> Note: See Lpackager [Quick Start](https://github.com/amranidev/lpackager#ii-quick-start)

#### Generate (Model,Migration,Controller)

All right, Now our **Client** package was created and registred.

Check if evreything is okey : 

`http://{your-project-url}/Client`  

Lests generate Model,Migration,Controller.

<br />

#### 1. Generate Model
	
Generate Person model : 

`php artisan lpackager:model Person kernel/Client "Kernel\Client"`
	
Result (kernel/Client/src/Person.php) :

```php

<?php

namespace Kernel\Client\Http\Controllers

use ClientAppController as Controller;

class PersonController extends Controller
{
	public function index()
	{
		//
	}
}

```

<br />

#### 2. Generate Migration
	
Generate Person migration : 

`php artisan make:migration persons --path=kernel/Client/database/migrations`
	
don't forget to change MigrationClass NameSpace to *Kernel\Client\database*.

<br />

#### 3. Generate Controller 

Generate PersonController :

`php artisan lpackager:controller PersonController Client Kernel/Client "Kernel\Client"`

Result (kernel/Client/src/Http/Controllers/PersonController.php) :

```php

<?php

namespace Kernel\Client\Http\Controllers

use ClientAppController as Controller;

class PersonController extends Controller
{
	public function index()
	{
		//
	}
}

```

<br />

Now we could create CRUD (Create,Read,Update,Delete) for *Person*, in the next article we're going to talk about how we could generate CRUD for packages, it will save a lot of time for us.