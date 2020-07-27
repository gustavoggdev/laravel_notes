# Seeders

Seeders tem a finalidade de gerar registros aleatórios na base de dados para efeito de teste.

#

Criando a Seeder 
```bash
php artisan make:seeder SeederName
```

Em cada Seeder temos o método *run* e dentro dele fica o código que deve ser executado quando executada a seeder

```php
public function run()
{
	DB::table('users')->insert([
		'first_name' => str_randon(10),
		'last_name' => str_randon(10),
		'email' => str_randon(10) . '@gmail.com',
		'password' => Hash::make('demo'),
		'status' => 'A'
	]);
}
```

#

Para executar somente uma seeder
```bash
php artisan db:seed --class=SeederName
```

#

Para executar todas as Seeders
```bash
php artisan db:seed
```
Esse comando executa todas as seeders que estão no arquivo DatabaseSeeder.php, dentro da basta **database/seeds/**
Então, caso execute o comando e não tenha retorno, verifica no arquivo DatabaseSeeder.php se não estão comentada as linhas de código com os nomes das Seeders

#

Caso precise dar um refresh nas migrations, há um parametros que após o refresh, executa todas as seeders
```bash
php artisan migrate:refresh --seed
```