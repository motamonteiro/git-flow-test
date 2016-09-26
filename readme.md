Segue abaixo o passo a passo das configurações para gerar a release 0.0.1:
 

Crie uma nova aplicação Laravel:

``` bash
laravel new minha-aplicacao
```

Configure o arquivo `.env`

Gere uma chave para a aplicação:
``` bash
php artisan key:generate
```

Verifique a instalação com o comando:

 ``` bash
php artisan serve
 ```

 Altere o nome da aplicação com o comando:

  ``` bash
 php artisan app:name MinhaAplicacao
  ```


Coloque as dependências do projeto no `composer.json` executando os seguintes passos:

``` bash
composer require prettus/l5-repository
```

``` bash
composer require league/fractal
```

``` bash
composer barryvdh/laravel-cors
```

Adicione `"prettus/laravel-validation": "1.1.*"` no composer.json

``` json
"require": {
        "php": ">=5.5.9",
        "laravel/framework": "5.2.*",
        "prettus/l5-repository": "^2.6",
        "prettus/laravel-validation": "1.1.*",
        "league/fractal": "^0.13.0",
        "barryvdh/laravel-cors": "^0.8.1"
    },
```

No seu `config/app.php` adicione `Prettus\Repository\Providers\RepositoryServiceProvider::class`  e `Barryvdh\Cors\ServiceProvider::class` no final do array providers:

``` php
'providers' => [
    ...
    Prettus\Repository\Providers\RepositoryServiceProvider::class,
    Barryvdh\Cors\ServiceProvider::class,
],
```

Publique a configuração

``` bash
php artisan vendor:publish
```

Crie o arquivo `app/Serializers/DataArraySerializer.php`

``` php
<?php

namespace MinhaAplicacao\Serializers;


use League\Fractal\Serializer\ArraySerializer;

class DataArraySerializer extends ArraySerializer
{

    /**
     * Serialize a collection.
     *
     * @param string $resourceKey
     * @param array  $data
     *
     * @return array
     */
    public function collection($resourceKey, array $data)
    {
        return $data;
        //return ["data" => $data];
    }
    /**
     * Serialize an item.
     *
     * @param string $resourceKey
     * @param array  $data
     *
     * @return array
     */
    public function item($resourceKey, array $data)
    {
        return $data;
        //return ["data" => $data];
    }

}
```

Altere o serializer do arquivo `config/repository.php`

``` php
'fractal'=>[
        'params'=>[
            'include'=>'include'
        ],
        'serializer' => \MinhaAplicacao\Serializers\DataArraySerializer::class
    ],
```

Rode a aplicação

``` bash
php artisan serve
```
