# Como funcionam as Rotas no Laravel 

As rotas são definidas nos arquivos existentes dentro do diretório routes (na v4 do Laravel era apenas um arquivo `routes.php`). <br>

Você pode definir rotas em qualquer verbo HTTP, veja exemplos:  <br>

```
Route::get($uri, $callback);
Route::post($uri, $callback);
Route::put($uri, $callback);
Route::patch($uri, $callback);
Route::delete($uri, $callback);
Route::options($uri, $callback);
```

Assim como também pode usar alguns métodos especiais: <br>

```
Route::any($uri, $callback); 
Route::resouce($uri, $callback);
```

O método `any` tratará qualquer tipo de requisição que chegar, seja ela de qual verbo HTTP for. <br>

O método `resource` automatiza o processo de construção do CRUD, mandando cada verbo para seu respectivo `method` dentro do controlador.


## Redirects - Redirecionamentos

Redirecionamento de rotas são feitos quando você precisa que um request HTTP seja enviado para outro destino. <br>

`Route::redirect('/daqui', '/pra-ca');`

Por padrão o status code é 302, mas você pode passar outro no terceiro parametro:<br>

`Route::redirect('/daqui', '/pra-ca', 302);`

## Route Parameters - Parâmetros de Rotas
Você precisará passar parâmetros para o controlador em algum momento, para isso você fará algo assim:

`Route::any(/clientes/{id}, 'clientesController@show); `

Isso faz com que qualquer requisição para o `/clientes/` com um `id`, será recebido pelo controlador `clientesController` no método `show`. Para isso funcionar, o método `show` deve aguardar um parâmetro:

`public function show($id) {}`

Pode precisar de multiplos parãmetros em algum momento, o processo seguirá sem dificuldade:

`Route::any(/clientes/{id}/pagamentos/{pagamento_id}, 'clientesController@show); `

E no controlador:

`public function show($id, $pagamento_id) {}`

### Parâmetros Opcionais
Para que o parâmetro seja opcional, você deve incluir um `?` a frente dele, veja:

`Route::any(/clientes/{id?}, 'clientesController@show); `

Não esqueça que para isso funcionar, o método do controlador tem que saber disso:

`public function show($id = null) {}`

## Named Routes - Rotas Nomeadas

Nomear as rotas faz com que você possa referenciá-las de forma mais simples, por exemplo, ao invés de toda vez ter que escrever o caminho completo em um redirecionamento, poderá apenas usar: `return redirect()->route('profile');`

Para usar este benefício, basta definir o nome na definição da rota:

```
Route::get('user/profile', 'UserProfileController@show')->name('profile');
```

Com isso, você pode usar os `helpers` especiais `route`e `url`. E no blade, por exemplo, construir links assim:

```
<a href="{{ url('user/profile', [1]) }}"> </a>

<a href="{{ route('routeName', ['id' => 1]) }}"> </a>
```

Se precisar saber qual é o nome da rota atual, você pode fazer isto:
```
$route = Route::current();
$name = $route->getName(); // Retorna o nome da Rota
$actionName = $route->getActionName(); // Retorna o método do controlador
```

## Route Groups - Grupo de Rotas

Você pode agrupar rotas para contextos específicos, por exemplo, determinadas rotas utilizarão determido middleware, sub-dominio, prefixo, etc. Exemplos:

### Rotas com subdomínios personalizados

```
Route::domain('{account}.myapp.com')->group(function () {
    Route::get('user/{id}', function ($account, $id) {
        //
    });
});
```

### Grupo de rotas nomeadas

```
Route::name('admin.')->group(function () {
    Route::get('users', 'usersController@index')->name('users');
    // Isso gera a rota nomeada como admin.users
});
```

### Rotas com o mesmo prefixo

```
Route::prefix('admin')->group(function () {
    Route::get('users', 'usersController@index')->name('users');
    Route::get('customers', 'customersController@index')->name('customers');
    // Isso gera as rotas users e customers dentro do contexto do admin, ou seja: /admin/users
});
```

### Combinando atributos para rotas

Você pode definir multiplos atributos na mesma definição de rotas

```
Route::group([
            'prefix'     => 'admin',
            'middleware' => [
                'auth',
                'anotherMiddleware',
                'yetAnotherMiddleware',
            ],
        ], function() {
            
           Route::get('dashboard', function() {} );
 });
```

----
to be continued ...

## Route Model Binding
## Rate Limiting
## Extra

Experimente rodar o comando `php artisan routes:list` para ver a lista de rotas que existem, assim como seus nomes, controladores e os verbos HTTP aceitos.