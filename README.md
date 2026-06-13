# Laravel Sensero (README فارسی)

`Laravel Sensero` 
یک داشبورد مانیتورینگ برای پروژه‌های Laravel است که اطلاعات سرور، وضعیت برنامه، ابزارهای نگهداری و چند ابزار عملیاتی را در یک پنل وب ارائه می‌دهد.

این فایل براساس بررسی کد پکیج در مسیر `packages/saeedvir/Laravel-Sensero` نوشته شده است.

## قابلیت‌ها

- مانیتورینگ لحظه‌ای مصرف CPU / RAM / Disk و نمودار مصرف
- نمایش اطلاعات سیستم، PHP، اکستنشن‌ها و پکیج‌های Laravel
- ویرایش `.env` (افزودن، حذف، بروزرسانی) با امکان بکاپ
- ویرایش فایل‌های `config/*.php` همراه با بررسی سینتکس
- اجرای دستورات Artisan، Composer و کلاس‌های داخلی سفارشی
- بررسی پردازش‌های دیتابیس و توقف پردازش‌ها
- مشاهده و مدیریت لاگ کوئری‌ها (کند / همه کوئری‌ها)
- نمایش Routeهای ثبت‌شده لاراول
- بررسی و اصلاح Permission فایل/پوشه‌های مهم پروژه
- مدیریت صف‌ها (Queue) و عملیات روی jobها
- بررسی اتصال اینترنت به چند endpoint و تست سرعت دانلود
- ویرایش `composer.json` از داخل پنل
- تغییر سریع حالت محیط بین `local` و `production` (طبق تنظیمات پکیج)

## نیازمندی‌ها

- PHP `^8.2`
- Laravel `^11.0 | ^12.0`

## نصب

### نصب از Packagist

```bash
composer require saeedvir/laravel-sensero
```

### نصب محلی (Path Repository)

در `composer.json` پروژه:

```json
{
  "repositories": [
    {
      "type": "path",
      "url": "../path/to/packages/laravel-sensero",
      "options": {
        "symlink": true
      }
    }
  ]
}
```
یا
```json
{
  "repositories": [
    {
      "type": "path",
      "url": "../path/to/packages/laravel-sensero"
    }
  ]
}
```
سپس:

```bash
composer require saeedvir/laravel-sensero:@dev
```

## راه‌اندازی

### 1) انتشار فایل تنظیمات

```bash
php artisan vendor:publish --provider="Saeedvir\LaravelSensero\LaravelSenseroServiceProvider" --tag="config"
```

### 2) انتشار assetها

```bash
php artisan vendor:publish --provider="Saeedvir\LaravelSensero\LaravelSenseroServiceProvider" --tag="assets"
```

### 3) انتشار فایل‌های زبان (اختیاری)

```bash
php artisan vendor:publish --provider="Saeedvir\LaravelSensero\LaravelSenseroServiceProvider" --tag="lang"
```

### 4) مسیر دسترسی

مسیر پیش‌فرض داشبورد:

- `/sensero`

(از طریق `LARAVEL_SENSERO_ROUTE_PREFIX` قابل تغییر است)

## تنظیمات مهم

فایل: `config/laravel-sensero.php`

نمونه گزینه‌های کلیدی:

```php
return [
    'route_prefix' => env('LARAVEL_SENSERO_ROUTE_PREFIX', '/sensero'),
    'language' => env('LARAVEL_SENSERO_LANGUAGE', env('APP_LOCALE', 'en')),
    'update_interval' => env('LARAVEL_SENSERO_UPDATE_INTERVAL', 25),
    'cache_ttl' => env('LARAVEL_SENSERO_CACHE_TTL', 25),
    'server_usage_enabled' => env('LARAVEL_SENSERO_USAGE_ENABLE', true),
    'command_logger' => env('LARAVEL_SENSERO_LOG_COMMAND', false),

    'database' => [
        'slow_query_threshold' => env('LARAVEL_SENSERO_QUERY_LOG_THRESHOLD', 300),
        'log_slow_queries' => env('LARAVEL_SENSERO_LOG_SLOW_QUERY', false),
        'log_any_queries' => env('LARAVEL_SENSERO_LOG_ANY_QUERY', false),
    ],

    'middleware' => ['web'],

    'security' => [
        'allowed_ips' => [],
        'authorize' => [
            'enable' => false,
            'admin_ids' => [],
            'auth_url' => null,
        ],
    ],
];
```

## امنیت و کنترل دسترسی

پکیج می‌تواند با سه لایه محدود شود:

- `middleware` (مثلاً `['web', 'auth']`)
- لیست IP مجاز (`security.allowed_ips`)
- احراز هویت و محدودیت شناسه کاربران (`security.authorize`)

نمونه پیشنهادی برای محیط production:

```php
'middleware' => ['web', 'auth'],

'security' => [
    'allowed_ips' => ['127.0.0.1', 'YOUR.SERVER.IP'],
    'authorize' => [
        'enable' => true,
        'admin_ids' => [1],
        'auth_url' => '/login',
    ],
],
```

## Queue ها

در پیاده‌سازی فعلی، `QueueManager` فقط درایور `database` را فعال می‌کند. اگر `queue.default` مقدار دیگری داشته باشد، Runtime Exception رخ می‌دهد.

برای استفاده از بخش Queue داشبورد، در `.env`:

```env
QUEUE_CONNECTION=database
```

## لاگ‌ها و فایل‌های مهم

- لاگ مصرف سرور: `storage/app/.server-status.log`
- لاگ کوئری کند: `storage/logs/slow_queries.log` (یا نام سفارشی)
- لاگ تمام کوئری‌ها: `storage/logs/all_queries.log` (یا نام سفارشی)
- لاگ اجرای commandها (در صورت فعال بودن): `storage/logs/commands.log`

## فرمان Artisan پکیج

```bash
php artisan sensero --mode=save-server-status
php artisan sensero --mode=clear-logs
```

- `save-server-status`: ذخیره وضعیت فعلی مصرف سرور
- `clear-logs`: پاکسازی لاگ‌های مربوط به پکیج

```php
use Illuminate\Support\Facades\Schedule;

Schedule::command('sensero', ['--mode' => 'save-server-status'])->everyMinute()
    ->withoutOverlapping() 
    ->onFailure(function () {
        Log::error('server status task failed.');
    });
```

## کلاس‌های داخلی سفارشی (Internal Commands)

برای افزودن Command داخلی در پنل:

1. یک کلاس بسازید که از `Saeedvir\LaravelSensero\Contracts\CommandExecute` ارث‌بری کند.
2. متدهای `title()` و `execute()` را پیاده‌سازی کنید.
3. کلاس را در `config('laravel-sensero.custom_commands.classes')` ثبت کنید.

## نکات مهم عملیاتی

- این پکیج قابلیت‌های حساسی مثل اجرای command، ویرایش `.env`، ویرایش `config` و تغییر `composer.json` دارد.
- در محیط production حتماً احراز هویت، محدودسازی IP و middleware مناسب را فعال کنید.
- فعال‌سازی لاگ همه کوئری‌ها (`LARAVEL_SENSERO_LOG_ANY_QUERY=true`) می‌تواند سربار قابل‌توجه ایجاد کند.

## مسیرهای اصلی

- `GET {route_prefix}/` برای نمایش داشبورد
- `GET|POST {route_prefix}/method/{method_name}` برای اکشن‌های AJAX داخلی

متدها در کنترلر با allow-list محدود شده‌اند و فقط نام‌های تعریف‌شده قابل فراخوانی هستند.

## لایسنس

برای تهیه لایسنس برنامه به وبسایت "آذران کد" مراجعه کنید

## ارتباط با نویسنده

- Saeed Abdollahian
- Email: `saeed.es91@gmail.com`
- Website: `https://azaran-code.ir`
