# Migrations

Comandos do Artisan para criações de Migrations no Laravel. [Documentação oficial](https://laravel.com/docs/7.x/migrations)

#

Criar uma migration com métodos *up* e *down* vazios
```bash
php artisan make:migration create_tableName_table
```

#

Criar migration com método *up* com nome da tabela, ID e timestamps e método *down* já fazendo o rollback
```bash
php artisan make:migration create_tableName_table --create=tableName
```

#

Criar migration para alteração de propriedade da tabela (adicionar coluna, editar tipo coluna etc)
```bash
php artisan make:migration add_column_columnName_tableName --table=tableName
```

#

Criar Model com uma migration relacionada com métodos *up* e *down* já preenchidos
```bash
php artisan make:model ModelName -m
```

#

Criar Model e Controller com todos os resources com a migration
```bash
php artisan make:model ModelName -rm
```

## Métodos Up e Down
São os métodos que serão executados quando acionar os comandos de migrate. O método *down* será sempre um comando contrário do método *up*, ou seja, um **rollback**

### Exemplo

Método *up*
```php
public function up()
{
    Schema::create('users', function (Blueprint $table) {
        $table->id();
        $table->string('first_name', 20);
        $table->string('last_name', 20);
        $table->string('email', 60);
        $table->string('password');
        $table->dateTime('email_verified_at');
        $table->string('status', 1);
        $table->timestamps();
    });
}
```

Método *down*
```php
public function down()
{
    Schema::dropIfExists('users');
}
```

## Relacionamentos

Para criar um relacionamento entre tabelas com as Foreign Keys, use o comando dentro do método *up*
```php
$table->unsignedInteger('columnName');
$table->foreign('columnName')->references('columnReference')->on('tableReference');
```
Pode ser também utilizado o ONDELETE ou ONUPDATE como CASCADE
```php
$table->unsignedInteger('columnName');
$table->foreign('columnName')->references('columnReference')->on('tableReference')->onDelete('cascade')->onUpdated('cascade');
```

## Executando Migrations

Executar todas as migrations que não não foram executadas
```bash
php artisan migrate
```

#

Fazer rollback das migrates já executadas. O parâmetro **--step** indica quando passos eu devo voltar nas migrates
O rollback executa os métodos *down* de cada migrate
```bash
php artisan migrate:rollback --step=3
```

#

Para fazer o rollback de todas as migrates, basta exeuctar o comando sem o parametro **step**
```bash
php artisan migrate:rollback
```

#

Existe a possibilidade de fazer o **refresh**, onde é executado todos os métodos *up* e *down* na ordem
Pode-se utilizar ou não o parâmetro **step**
```bash
php artisan migrate:refresh --step=1
```
