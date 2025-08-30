<p align="center">
    <a href="https://gp247.net"><img src="https://static.gp247.net/logo/logo.png" width="150"></a>
</p>
<p align="center">Free and open-source eCommerce website<br>
    <code><b>composer create-project gp247/s-cart</b></code></p>
<p align="center">
 <a href="https://s-gp247.net">Homepage</a> | <a href="https://demo.s-cart.org">Demo</a> | <a href="https://gp247.net/en/docs/s-cart/s-cart-overview.html">Documentation</a>  | <a href="https://www.facebook.com/groups/scart.opensource">Facebook Group</a>
</p>

<p align="center">
<a href="https://packagist.org/packages/gp247/s-cart"><img src="https://poser.pugx.org/gp247/s-cart/d/total" alt="Packagist Downloads"></a>
<a href="https://github.com/gp247net/s-cart/releases"><img src="https://poser.pugx.org/gp247/s-cart/v/stable.svg" alt="Latest Stable Version"></a>
<a href="https://github.com/gp247net/s-cart/blob/master/LICENSE"><img src="https://poser.pugx.org/gp247/s-cart/license" alt="License"></a>
</p>


## About S-Cart
S-Cart is a free eCommerce website project for individuals and businesses, built on top of the Laravel Framework and modern technologies.
Our goal is "Efficient and friendly for everyone":
- Efficient: Satisfy even the smallest customer requirements.
- Friendly: Easy to use, maintain, and extend.
- Everyone: Businesses, individuals, developers, students.

[New versions of S-Cart since 2025 are developed by the GP247 team]

About components:

> **S-Cart** = `Laravel` + `GP247/Core` + `GP247/Front` + `GP247/Shop`

## Screenshots
<img src="https://static.s-cart.org/guide/use/common/shop.jpg">
<img src="https://static.s-cart.org/guide/use/common/dashboard.jpg">

## S-Cart features

### S-Cart - FREE eCommerce website solution for businesses

#### Core capabilities
- HMVC-based plugin package architecture
- Upgrade and patch S-Cart via CLI
- Full documentation for developers and customers

#### Professional eCommerce features
- **Multi-language**
- **Multi-currency**
- **Full eCommerce capabilities:**
  - Cart management
  - Order management
  - Product management
  - Customer management
- **CMS content management:**
  - Categories
  - News/Blog
  - Content pages
- **Extensions:**
  - Payment plugins
  - Shipping methods
  - Discount system
  - Tax calculation
- **Professional plugins for S-Cart:**
  - Multi-vendor: https://gp247.net/en/docs/s-cart/multi-vendor.html
  - Multi-stores: https://gp247.net/en/docs/s-cart/multi-store.html
- **Developer resources:**
  - Online library: plugins and templates
  - API with auth for mobile and integration

#### Powerful administration features
- **User management:**
  - Role-based permissions (admin, manager, marketing, etc.)
  - Comprehensive security with full logging
  - Access control, authentication, and CAPTCHA
- **Business tools:**
  - Product management
  - Order processing
  - Customer management
  - Analytics and reports
  - Activity tracking


## S-Cart 1.x

> Powered by the GP247 ecosystem <a href="https://github.com/gp247net">https://github.com/gp247net</a>

> Core Laravel framework 12.x <a href="https://github.com/laravel/laravel">https://github.com/laravel/laravel</a>


## Project structure using GP247

    Website-folder/
    |
    ├── app
    │     └── GP247
    │           ├── Core(+) //Customize Core controllers
    │           ├── Helpers(+) //Auto-load Helpers/*.php into the system
    │           ├── Front(+) //Customize GP247/Front controllers
    │           ├── Shop(+) //Customize GP247/Shop controllers
    │           ├── Plugins(+) //Use `php artisan gp247:make-plugin --name=NameOfPlugin`
    │           └── Templates(+) //Use `php artisan gp247:make-template --name=NameOfTempate`
    ├── public
    │     └── GP247
    │           ├── Core(+)
    │           ├── Plugins(+)
    │           └── Templates(+)
    ├── resources
    │            └── views/vendor
    │                           |── gp247-core(+) //Customize core views
    │                           └── gp247-front(+) //Customize front views
    ├── vendor
    │     ├── gp247/core
    │     ├── gp247/front
    │     └── gp247/shop
    └──...


## Quick installation guide

### Method 1: Install via Composer (Recommended)

- Step 1:

  Command:
  >`composer create-project gp247/s-cart`

- Step 2: Check configuration in .env

  Ensure your database configuration and APP_KEY in .env are properly set.

  If APP_KEY is not set, generate one:
  >`php artisan key:generate`

- Step 3: Initialize S-Cart

  Run:
  >`php artisan sc:install`

- Step 4: Install sample data (optional)

  If you want sample data, run:
  >`php artisan sc:sample`

### Method 2: Install via Git Clone

- Step 1: Clone repository from GitHub

  >`git clone https://github.com/gp247net/s-cart.git`

- Step 2: Move into project folder

  >`cd s-cart`

- Step 3: Create .env from example

  >`cp .env.example .env`

- Step 4: Generate APP_KEY

  >`php artisan key:generate`

- Step 5: Install dependencies via Composer

  >`composer install`

- Step 6: Configure database in .env

  Edit database connection in .env:
  ```
  DB_CONNECTION=mysql
  DB_HOST=127.0.0.1
  DB_PORT=3306
  DB_DATABASE=your_database_name
  DB_USERNAME=your_username
  DB_PASSWORD=your_password
  ```

- Step 7: Initialize S-Cart

  >`php artisan sc:install`

- Step 8: Install sample data (optional)

  >`php artisan sc:sample`

### Method 3: Install each component (Laravel + GP247/Core + GP247/Front + GP247/Shop)

- Step 1: Create a Laravel 12.x project (or use an existing one)

  >`composer create-project laravel/laravel s-cart`

- Step 2: Change into the s-cart folder and install GP247 components in order

  >`composer require gp247/core`

  >`composer require gp247/front`

  >`composer require gp247/shop`

- Step 3: Register Service Providers

  Open `bootstrap/providers.php`, add these 2 providers to the end of the returned array:

  ```php
  GP247\Front\FrontServiceProvider::class,
  GP247\Shop\ShopServiceProvider::class,
  ```

- Step 4: Configure routing and exceptions for GP247

  Open `bootstrap/app.php`:

  - Comment out the web routes line:

    ```php
    //GP247 comment
    //web: __DIR__.'/../routes/web.php',
    ```

  - Add exception handling (place inside the exceptions configuration block):

    ```php
    // GP247 add new
    $exceptions->report(function (\Throwable $e) {
        if (function_exists('gp247_handle_exception')) {
            gp247_handle_exception($e);
        }
    });
    ```

- Step 5: Generate APP_KEY if not yet present

  >`php artisan key:generate`

- Step 6: Configure database in .env

  Edit database connection in .env:
  ```
  DB_CONNECTION=mysql
  DB_HOST=127.0.0.1
  DB_PORT=3306
  DB_DATABASE=your_database_name
  DB_USERNAME=your_username
  DB_PASSWORD=your_password
  ```

- Step 7: Run the following commands in sequence to install

  >`php artisan gp247:core-install`

  >`php artisan gp247:front-install`

  >`php artisan gp247:shop-install`

- Step 8: Install sample data (optional)

  >`php artisan gp247:shop-sample`

### Important folder permissions

Ensure the following folders are writable:
- `app/GP247`
- `public/GP247`
- `public/vendor`
- `resources/views/vendor`
- `storage`
- `vendor`

If write permissions are incorrect, installation and various features may not work properly.

## Useful information

**Check S-Cart version**

(Only available when installing S-Cart directly)

>`php artisan sc:info`

**Update S-Cart**

Update packages:

(Only available when installing S-Cart directly)

>`composer update gp247/core`

>`composer update gp247/front`

>`composer update gp247/shop`

Then run:

>`php artisan sc:update`

**Create plugin:**

>`php artisan gp247:make-plugin  --name=PluginName`

Create plugin zip file:

>`php artisan gp247:make-plugin  --name=PluginName --download=1`

**Create template:**

>`php artisan gp247:make-template  --name=TemplateName`

Create template zip file:

>`php artisan gp247:make-template  --name=TemplateName --download=1`

## Customization

**Publish lfm config for uploads**

>`php artisan vendor:publish --tag=config-lfm`

**Customize core admin views**

>`php artisan vendor:publish --tag=gp247:view-core`

**Override gp247_* helper functions**

>Step 1: Add the list of functions you want to override to `config/gp247_functions_except.php`

>Step 2: Create new PHP files containing the new functions in `app/GP247/Helpers`, e.g. `app/GP247/Helpers/myfunction.php`

**Override gp247 controllers**

>Step 1: Copy the controller files you want to override from vendor/gp247/core/src/Core/Controllers -> app/GP247/Core/Controllers

>Step 2: Change `namespace GP247\Core\Controllers` to `namespace App\GP247\Core\Controllers`

**Override gp247 API controllers**

>Step 1: Copy the controller files you want to override from vendor/gp247/core/src/Api/Controllers -> app/GP247/Core/Api/Controllers

>Step 2: Change `namespace GP247\Core\Api\Controllers` to `namespace App\GP247\Core\Api\Controllers`

## Add routes

Use the prefix and middleware constants `GP247_ADMIN_PREFIX`, `GP247_ADMIN_MIDDLEWARE` in route declarations.

Reference: https://github.com/gp247net/core/blob/master/src/routes.php


## Environment variables in .env

**Disable API**
> `GP247_API_MODE=1` // Set 0 to disable

**Database table prefix**
> `GP247_DB_PREFIX=gp247_` // Cannot be changed after gp247 installation

**Admin path prefix**
> `GP247_ADMIN_PREFIX=gp247_admin`

