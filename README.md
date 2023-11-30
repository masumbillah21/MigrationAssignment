# Assignment 10

## Task 1

Create a new Laravel project named "MigrationAssignment" using the Laravel command-line interface.

```Terminal
composer create-project laravel/laravel MigrationAssignment
```

or

```Terminal
laravel new MigrationAssignment
```

## Task 2

Within the project, create a new migration file named "create_products_table" that will be responsible for creating a table called "products" in the database. The "products" table should have the following columns:

```Terminal
php artisan make:migration create_products_table
```

- id: an auto-incrementing integer and primary key.
- name: a string column to store the product name.
- price: a decimal column to store the product price.
- description: a text column to store the product description.
- created_at: a timestamp column to store the creation date and time.
- updated_at: a timestamp column to store the last update date and time.

```php
Schema::create('products', function (Blueprint $table) {
    $table->integer('id')->autoIncrement();
    $table->string('name');
    $table->decimal('price');
    $table->text('description');
    $table->timestamp('created_at')->useCurrent();
    $table->timestamp('updated_at')->useCurrent()->useCurrentOnUpdate();
});
```

## Task 3

After creating the migration file, run the migration to create the "products" table in the database.

```Terminal
php artisan migrate   
```

## Task 4

Modify the existing migration file "create_products_table" to add a new column called "quantity" to the "products" table. The "quantity" column should be an integer column and allow null values.

```php
Schema::create('products', function (Blueprint $table) {
    $table->integer('id')->autoIncrement();
    $table->string('name');
    $table->decimal('price');
    $table->text('description');
    $table->integer('quantity')->nullable();
    $table->timestamp('created_at')->useCurrent();
    $table->timestamp('updated_at')->useCurrent()->useCurrentOnUpdate();
});
```

After modify existing file run

```Terminal
php artisan migrate:refresh
```

## Task 5

Create a new migration file named "add_category_to_products_table" that will be responsible for adding a new column called "category" to the "products" table. The "category" column should be a string column with a maximum length of 50 characters.

```Terminal
php artisan make:migration add_category_to_products_table
```

```php
Schema::table('products', function (Blueprint $table) {
    $table->string('category', 50)->after('quantity'); //->after('description') optional here
});
```

## Task 6

After creating the new migration file, run the migration to add the "category" column to the "products" table.

```Terminal
php artisan migrate   
```

## Task 7

Create a new migration file named "create_orders_table" that will be responsible for creating a table called "orders" in the database. The "orders" table should have the following columns:

```Terminal
php artisan make:migration create_orders_table
```

- id: an auto-incrementing integer and primary key.
- product_id: an unsigned integer column to establish a foreign key relationship with the "id" column of the "products" table.
- quantity: an integer column to store the quantity of products ordered.
- created_at: a timestamp column to store the creation date and time.
- updated_at: a timestamp column to store the last update date and time.

```php
Schema::create('orders', function (Blueprint $table) {
    $table->integer('id')->autoIncrement();
    $table->integer('product_id');
    $table->foreign('product_id')->references('id')->on('products');
    $table->integer('quantity');
    $table->timestamp('created_at')->useCurrent();
    $table->timestamp('updated_at')->useCurrent()->useCurrentOnUpdate();
});
```

## Task 8

After creating the migration file for the "orders" table, run the migration to create the "orders" table in the database

```Terminal
php artisan migrate
```
