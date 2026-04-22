# OpenCart — Disable Storage Warning

## The Warning

When logging into the OpenCart admin panel you may see:

> "It is very important that you move the storage directory outside of the web directory."

In **production** this should be fixed properly by moving the storage folder outside of `public_html`. In **local development** you can disable it.

---

## How to Disable (Dev Only)

Open the file:

```
admin/controller/common/dashboard.php
```

Find this block:

```php
if (DIR_STORAGE == DIR_SYSTEM . 'storage/') {
    $data['security'] = $this->load->controller('common/security');
} else {
    $data['security'] = '';
}
```

Replace it with:

```php
$data['security'] = '';
```

---

## Production Fix

On a live server, move the storage folder **outside** of `public_html`:

```
/home/username/storage/   ← correct (not web accessible)
/home/username/public_html/system/storage/  ← wrong
```

Then update both `config.php` and `admin/config.php`:

```php
define('DIR_STORAGE', '/home/username/storage/');
```

---

> ⚠️ **Never disable this warning in production** — only in local dev environments.
