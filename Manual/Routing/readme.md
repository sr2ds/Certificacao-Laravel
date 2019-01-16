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

----
to be continued ...

## Named Routes

## Route Groups
## Route Model Binding
## Rate Limiting