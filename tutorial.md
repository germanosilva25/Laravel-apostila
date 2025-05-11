# Apostila de Laravel

## Introdução ao PHP e ao Funcionamento de Servidores Web

Antes de entender como o Laravel funciona, é fundamental compreender o funcionamento do PHP, pois o Laravel é um framework baseado nessa linguagem de programação.

### Funcionamento do PHP em Servidores Web

Servidores web que utilizam PHP geralmente procuram, por padrão, um arquivo chamado `index.php` na pasta principal da aplicação ou em suas subpastas. Suponha que você tenha acabado de instalar o XAMPP. Nesse caso, toda vez que o servidor for acessado pela porta 80 (padrão HTTP), ele buscará automaticamente o arquivo `index.php` dentro da pasta `htdocs`, caso o nome do arquivo não tenha sido especificado na URL.

Vamos analisar isso por partes:

* Ao acessar `http://localhost/`, o servidor buscará por `htdocs/index.php`.
* Caso você acesse uma subpasta, como `http://localhost/fotos/`, o servidor procurará por `htdocs/fotos/index.php`.
* Se não encontrar o arquivo, será exibida uma mensagem de erro 404 (página não encontrada).

A URL pode ser escrita diretamente com o nome do arquivo, por exemplo:

```
http://localhost/minhas-fotos.php
```

Nesse caso, deve existir um arquivo chamado `minhas-fotos.php` dentro da pasta `htdocs`.

Resumidamente, uma URL em PHP é composta por:

* O domínio (ex: `localhost`)
* As pastas que compõem a estrutura da aplicação
* O nome do arquivo, que pode ser omitido se for `index.php`

---

## Introdução ao Laravel

Agora que você entendeu como o PHP funciona, vamos conhecer a estrutura básica do Laravel.

Na pasta principal do Laravel existe um arquivo chamado `index.php`, localizado dentro da pasta `public/`. Esse arquivo é o ponto de entrada da aplicação e é responsável por iniciar o carregamento do framework.

O Laravel segue a arquitetura MVC (Model-View-Controller), e a definição das rotas da aplicação é feita no arquivo `routes/web.php`. É nele que indicamos quais URLs estarão disponíveis para o usuário.

### Criando sua primeira rota

Vamos supor que você queira criar uma página que lista usuários. Para isso, siga os passos abaixo:

1. **Defina a rota no arquivo `routes/web.php`:**

```php
use App\Http\Controllers\UserController;

Route::get('/usuarios', [UserController::class, 'getUsuarios']);
```

2. **Crie o controller correspondente:**

Crie um arquivo chamado `UserController.php` em `app/Http/Controllers/` com o seguinte conteúdo:

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Foundation\Auth\Access\AuthorizesRequests;
use Illuminate\Foundation\Bus\DispatchesJobs;
use Illuminate\Foundation\Validation\ValidatesRequests;
use Illuminate\Routing\Controller as BaseController;

class UserController extends BaseController
{
    use AuthorizesRequests, DispatchesJobs, ValidatesRequests;

    public function getUsuarios()
    {
        return response()->json([
            ["id" => 1, "nome" => "Karol", "nome_grupo" => "admin"],
            ["id" => 2, "nome" => "Nathy", "nome_grupo" => "profissional"],
            ["id" => 3, "nome" => "Hanna", "nome_grupo" => "profissional"],
            ["id" => 4, "nome" => "Germano", "nome_grupo" => "profissional"],
            ["id" => 5, "nome" => "Cauê", "nome_grupo" => "profissional"],
            ["id" => 6, "nome" => "Flávia", "nome_grupo" => "cliente"],
            ["id" => 7, "nome" => "Bruno", "nome_grupo" => "cliente"],
            ["id" => 8, "nome" => "Josué", "nome_grupo" => "cliente"],
            ["id" => 9, "nome" => "Matheus", "nome_grupo" => "cliente"],
            ["id" => 10, "nome" => "Ludi", "nome_grupo" => "cliente"]
        ]);
    }
}
```

3. **Teste a rota:**

Abra o navegador e acesse `http://localhost/usuarios`. Você verá a lista de usuários sendo exibida no formato JSON.

---

## O que é o MVC (Model-View-Controller)?

O Laravel utiliza o padrão arquitetural MVC para organizar o código.

### Model (Modelo)

Representa os dados da aplicação e sua lógica de negócio. No Laravel, normalmente são classes Eloquent que interagem com o banco de dados.

👉 Exemplo: Um modelo `User` que representa a tabela de usuários no banco.

### View (Visão)

Responsável pela interface com o usuário. Exibe os dados e recebe entradas. Laravel usa o mecanismo de templates Blade para isso.

👉 Exemplo: Um arquivo `usuarios.blade.php` que mostra a lista de usuários em uma página HTML.

### Controller (Controlador)

Recebe as requisições HTTP, processa com ajuda dos Models e retorna uma resposta (View ou JSON).

👉 Exemplo: O `UserController` com o método `getUsuarios` que retorna a lista de usuários.

---

Com isso, você tem uma base sólida para começar a construir aplicações com Laravel!
