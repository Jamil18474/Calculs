<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

<p align="center">
<a href="https://travis-ci.org/laravel/framework"><img src="https://travis-ci.org/laravel/framework.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>


## Rôles
Il y'a trois rôles: Member, Admin et Superadmin
Member n'a aucun priviliège et n'a le droit qu'à consulter certains modèles
```
{
    "name": "member",
    "email": "member@member.com",
    "password": "utilisateur",
    "role": "member",
}
```
Admin a le droit de consulter tous les modèles, de modifier, créer des modèles mais pas de supprimer les modèles
```
{
    "name": "admin",
    "email": "admin@admin.com",
    "password": "administrateur",
    "role": "admin"
}
```

SuperAdmin a tous les droits sur tous les modèles.
```
{
    "name": "superadmin",
    "email": "superadmin@superadmin.com",
    "password": "superadmin",
    "role": "superadmin"
}
```
On peut définir le rôle d'un utilisateur en utilisant une énumération de 3 valeurs définis dans la bse de données : soit "member" soit "admin" soit "superadmin"
De base les utilisateurs sont "member"
Il faut changer d'abord dans la base de donnée pour qu'il soit admin ou superadmin

## Postman
Toutes les requêtes sont sur le Postman partagé par mail
Pour récupérer le bearer token pour tester les requêtes il faut être soit admin soit superadmin et faire une requête en POST 
Pour la requête de mise à jour(update) d'un instrument j'ai dû utiliser post pour avoir accès au form-data car je charge une image mais j'ai précisé _method PATCH dans le form-data.

## Routes côté API
```
// Users

    Route::apiResource('/users', UserController::class);
    Route::post('/users/search', [RayonController::class, 'search']);

    // Instruments

    Route::apiResource('/instruments', InstrumentController::class);
    Route::post('/instruments/search', [InstrumentController::class, 'search']);
    
    // Marques
    Route::apiResource('/marques', MarqueController::class);
    Route::post('/marques/search', [MarqueController::class, 'search']);
    //Types

   
    Route::apiResource('/types', TypeController::class);
    Route::post('/types/search', [TypeController::class, 'search']);


    //Employés

    Route::apiResource('/employes', EmployeController::class);
    Route::post('/employes/search', [EmployeController::class, 'search']);

    // Promotions

    Route::apiResource('/promotions', PromotionController::class);
    Route::post('/promotions/search', [PromotionController::class, 'search']);

    // Rayons

    Route::apiResource('/rayons',RayonController::class);
    Route::post('/rayons/search', [RayonController::class, 'search']);
```

## Routes côté Back-office
```
    Route::get('/instruments', [InstrumentController::class,'index'])
        ->name('instruments.index');

    Route::get('/instruments/create', [InstrumentController::class,'create'])
        ->name('instrument.create');

    Route::post('/instruments', [InstrumentController::class,'store'])
        ->name('instrument.store');

    Route::get('/instrument/{instrument}', [InstrumentController::class,'show'])
        ->where('instrument', '[0-9]+')
        ->name('instrument.show');

    Route::get('/instrument/{instrument}/edit', [InstrumentController::class, 'edit'])
        ->where('instrument', '[0-9]+')
        ->name('instrument.edit');

    Route::patch('/instrument/{instrument}', [InstrumentController::class, 'update'])
        ->where('instrument', '[0-9]+')
        ->name('instrument.update');

    Route::delete('/instrument/{instrument}', [InstrumentController::class, 'destroy'])
        ->where('instrument', '[0-9]+')
        ->name('instrument.delete');
    
    // Marques

    Route::get('/marques', [MarqueController::class,'index'])
        ->name('marques.index');

    Route::get('/marques/create', [MarqueController::class,'create'])
        ->name('marque.create');

    Route::post('/marques', [MarqueController::class,'store'])
        ->name('marque.store');

    Route::get('/marque/{marque}', [MarqueController::class,'show'])
        ->where('marque', '[0-9]+')
        ->name('marque.show');

    Route::get('/marque/{marque}/edit', [MarqueController::class, 'edit'])
        ->where('marque', '[0-9]+')
        ->name('marque.edit');

    Route::patch('/marque/{marque}', [MarqueController::class, 'update'])
        ->where('marque', '[0-9]+')
        ->name('marque.update');

    Route::delete('/marque/{marque}', [MarqueController::class, 'destroy'])
        ->where('marque', '[0-9]+')
        ->name('marque.delete');
    
    //Types

    Route::get('/types', [TypeController::class,'index'])
        ->name('Types.index');

    Route::get('/types/create', [TypeController::class,'create'])
        ->name('type.create');

    Route::post('/types', [TypeController::class,'store'])
        ->name('type.store');

    Route::get('/type/{type}', [TypeController::class,'show'])
        ->where('type', '[0-9]+')
        ->name('type.show');

    Route::get('/type/{type}/edit', [TypeController::class, 'edit'])
        ->where('type', '[0-9]+')
        ->name('type.edit');

    Route::patch('/type/{type}', [TypeController::class, 'update'])
        ->where('type', '[0-9]+')
        ->name('type.update');

    Route::delete('/type/{type}', [TypeController::class, 'destroy'])
        ->where('type', '[0-9]+')
        ->name('type.delete');

    //Employés

    Route::get('/employes', [EmployeController::class,'index'])
        ->name('employes.index');

    Route::get('/employes/create', [EmployeController::class,'create'])
        ->name('employe.create');

    Route::post('/employes', [EmployeController::class,'store'])
        ->name('employe.store');

    Route::get('/employe/{employe}', [EmployeController::class,'show'])
        ->where('employe', '[0-9]+')
        ->name('employe.show');

    Route::get('/employe/{employe}/edit', [EmployeController::class, 'edit'])
        ->where('employe', '[0-9]+')
        ->name('employe.edit');

    Route::patch('/employe/{employe}', [EmployeController::class, 'update'])
        ->where('employe', '[0-9]+')
        ->name('employe.update');

    Route::delete('/employe/{employe}', [EmployeController::class, 'destroy'])
        ->where('employe', '[0-9]+')
        ->name('employe.delete');

    // Promotions

    Route::get('/promotions', [PromotionController::class,'index'])
        ->name('promotions.index');

    Route::get('/promotions/create', [PromotionController::class,'create'])
        ->name('promotion.create');

    Route::post('/promotions', [PromotionController::class,'store'])
        ->name('promotion.store');

    Route::get('/promotion/{promotion}', [PromotionController::class,'show'])
        ->where('promotion', '[0-9]+')
        ->name('promotion.show');

    Route::get('/promotion/{promotion}/edit', [PromotionController::class, 'edit'])
        ->where('promotion', '[0-9]+')
        ->name('promotion.edit');
        
    Route::patch('/promotion/{promotion}', [PromotionController::class, 'update'])
        ->where('promotion', '[0-9]+')
        ->name('promotion.update');

    Route::delete('/promotion/{promotion}', [PromotionController::class, 'destroy'])
        ->where('promotion', '[0-9]+')
        ->name('promotion.delete');

    // Rayons

    Route::get('/rayons', [RayonController::class,'index'])
        ->name('rayons.index');

    Route::get('/rayons/create', [RayonController::class,'create'])
        ->name('rayon.create');

    Route::post('/rayons', [RayonController::class,'store'])
        ->name('rayon.store');

    Route::get('/rayon/{rayon}', [RayonController::class,'show'])
        ->where('rayon', '[0-9]+')
        ->name('rayon.show');

    Route::get('/rayon/{rayon}/edit', [RayonController::class, 'edit'])
        ->where('rayon', '[0-9]+')
        ->name('rayon.edit');

    Route::patch('/rayon/{rayon}', [RayonController::class, 'update'])
        ->where('rayon', '[0-9]+')
        ->name('rayon.update');

    Route::delete('/rayon/{rayon}', [RayonController::class, 'destroy'])
        ->where('rayon', '[0-9]+')
        ->name('rayon.delete');
        

    //Users
        
    Route::get('/users', [UserController::class,'index'])
        ->name('users.index');

    Route::get('/user/{user}', [UserController::class,'show'])
        ->where('user', '[0-9]+')
        ->name('user.show');

    Route::get('/user/{user}/edit', [UserController::class, 'edit']) #utilise la méthode edit de la classe Usercontroller
        ->where('user', '[0-9]+')
        ->name('user.edit');

    Route::patch('/user/{user}', [UserController::class, 'update'])
        ->where('user', '[0-9]+')
        ->name('user.update');

    Route::delete('/user/{user}', [UserController::class, 'destroy'])
        ->where('user', '[0-9]+')
        ->name('user.delete');;
```