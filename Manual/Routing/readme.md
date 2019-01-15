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

----
to be continued ...

## Route Parameters
## Named Routes
## Route Groups
## Route Model Binding
## Rate Limiting