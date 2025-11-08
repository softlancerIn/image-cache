# 🖼️ Intervention Image Cache (Modern Fork)

> ⚙️ **A modern maintained fork** of the original [Intervention Image Cache](https://github.com/Intervention/imagecache) package.
> 🚧 The original package has been **abandoned**, so this version focuses on maintaining stability and compatibility with modern PHP and Laravel versions.

---

### ⚠️ Important Notes

> **⚠️ CAUTION:**
> This package is currently **unstable**, as it still depends on the original `intervention/image` package for certain configurations (like the config path).

---

## 📦 Overview

**Intervention Image Cache** extends the core [Intervention Image](https://github.com/Intervention/image/) functionality by adding **powerful caching capabilities** for optimized image handling.

It integrates seamlessly with [Illuminate/Cache](https://github.com/illuminate/cache/) — making it easy to use with the [Laravel Framework](https://laravel.com/). Depending on your cache configuration, it supports:

* 🗂️ Filesystem
* 🧠 Database
* ⚡ Memcached
* 🔥 Redis

💡 **How it works:**
Each image manipulation is tracked and cached. If the same sequence of operations is requested again, the cached result is returned instead of processing the image again — saving time and resources.

---

## 🚀 Installation

Install the package via Composer:

```bash
composer require softlancerin/image-cache:dev-master
```

Once installed, make sure to include Composer’s autoload file if not already:

```php
require 'vendor/autoload.php';
```

---

## ⚡ Laravel Integration

To use **Intervention Image Cache** with Laravel, register the Service Provider and Facade in your `config/app.php` file.

### Add to the `providers` array:

```php
'providers' => [
    // ...
    Intervention\Image\ImageServiceProvider::class,
],
```

That’s it! 🎉
You can now use the `Image` facade for caching operations within your Laravel application.

---

## 🧩 Usage Example

Use the static method `Image::cache()` to perform image operations with automatic caching.

### Basic Example

```php
use Intervention\Image\Facades\Image;

$img = Image::cache(function($image) {
    return $image->make('public/foo.jpg')->resize(300, 200)->greyscale();
});
```

### With Cache Lifetime

You can define the cache lifetime (in minutes) and optionally return an **Image object** instead of a stream.

```php
$img = Image::cache(function($image) {
    return $image->make('public/foo.jpg')->resize(300, 200)->greyscale();
}, 10, true);
```

---

## 🌐 Server Configuration (Nginx Example)

If you’re using **Nginx** and have static resource caching enabled, make sure to **exclude your cache directory** (defined in your config, e.g., `/cache`) from static caching:

```nginx
# Exclude "cache" directory from static caching
location ~* ^\/(?!cache).*\.(?:jpg|jpeg|gif|png|ico|cur|gz|svg|svgz|mp4|ogg|ogv|webm|htc|webp|woff|woff2)$ {
    expires max;
    access_log off;
    add_header Cache-Control "public";
}
```

---

## 🛠️ Handled & Supported By

> 🧩 **This modern fork is handled and actively supported by [Softlancerin](https://github.com/softlancerin)** —
> empowering open-source PHP & Laravel development with modern solutions and community-driven updates.

---

## 📜 License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT).
Use it freely for both commercial and personal projects.

---

### 💡 Maintained By

**Softlancerin Innovations** — modernizing PHP packages for the developer community.
⭐ Feel free to star this repo if you find it helpful!