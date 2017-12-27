# .env 檔案

## Laravel 4 .env 檔案

在 Laravel 4 的時候，我們通常會在 `/bootstrap/start.php` 中，去設定我們的 `hostname` 是屬於哪一種開發環境，再針對不同的開發環境有不同的設定檔（`.env.*.php`）

```php
<?php
$env = $app->detectEnvironment(array(
  'local' => array(
    'KeJyun-Macbook'
  ),
  'dev' => [],
  'testing' => [],
  'staging' => [],
));
```

`.env.*.php` 設定檔通常放在根目錄下，這些檔案不會在版本控制當中

```
app/
bootstrap/
public/
vendor/
.env.php
.env.local.php
.env.dev.php
.env.testing.php
.env.staging.php
```

在 Laravel 4 .env 設定檔案長的會像是這樣：

```php
<?php
return [
  'DB_USERNAME' => 'root',
  'DB_PASSWORD' => 'password',
];
```

我們的 `config` 檔案就可以使用 `$_ENV` 去讀取當前環境的設定檔資料

```php
<?php
$_ENV['DB_USERNAME']
$_ENV['DB_PASSWORD']
```

## Laravel 5 .env 檔案

在 Laravel 5 使用 `.env` 檔案的方式跟 Laravel 4 有很大的不同，在 Laravel 5 中就只有 `.env` 與 `.env.example` 這兩個檔案而已，`.env` 檔案不會在版本控制中，`.env.example` 則會在版本控制中

自己可以根據自己的環境設定目前的 .env 狀況，而 .env.example 則是可以讓大家參考 .env 的範例用的，自己根據自己目前的環境設定是什麼樣到開發還境（local、dev、stage、production...etc）。


在 Laravel 5 .env 設定檔案長的會像是這樣：

```
APP_ENV=local
APP_DEBUG=true
APP_KEY=VDqhX1LiHKEReHH16YNEzxUZziOdZVtT

DB_HOST=localhost
DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret

CACHE_DRIVER=file
SESSION_DRIVER=file
```

然後我們在設定檔中，我們可以使用 `env()` 函式去取得我們設定檔案中的設定，會設定像是這樣的設定

```php
// config/app.php
[
  'debug' => env('APP_DEBUG', false),
]

// config/database.php
[  
  'pgsql' => [
      'driver'   => 'pgsql',
      'host'     => env('DB_HOST', 'localhost'),
      'database' => env('DB_DATABASE', 'forge'),
      'username' => env('DB_USERNAME', 'forge'),
      'password' => env('DB_PASSWORD', ''),
      'charset'  => 'utf8',
      'prefix'   => '',
      'schema'   => 'public',
  ],
]
```

`env()` 中第一個參數是 `.env` 檔案中的設定鍵值名稱，第二個參數是預設值，若讀取不到環境設定鍵值則會使用預設值

這樣在每個人的開發環境只要去管理自己的 `.env` 檔案就好，不需要像 Laravel 4 需要在 config 資料夾中建立各種環境變數設定的資料夾，像是 `config/local/database.php` 或 `config/stage/database.php`。

## 參考資料
* [Environments and Configuration - Laravel 5 Fundamentals](https://laracasts.com/series/laravel-5-fundamentals/episodes/6)

!INCLUDE "../kejyun/book/laravel-5-for-beginner.md"
