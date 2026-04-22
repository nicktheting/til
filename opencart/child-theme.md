# OpenCart — Child Theme

## What is a Child Theme

OpenCart uses a **fallback system** — if a template file is not found in your custom theme, the system automatically loads it from the `default` theme. This means you only need to copy and modify the files you want to change.

---

## Folder Structure

```
catalog/view/theme/
    ├── default/          ← Parent theme (never touch this)
    └── mytheme/          ← Child theme (work here)
        ├── template/     ← Twig template files
        ├── stylesheet/   ← CSS files
        └── javascript/   ← JS files
```

---

## Step 1 — Create the folder

```
C:\laragon\www\opencart\catalog\view\theme\mytheme
```

Inside `mytheme` create these folders:

```
mytheme/
├── template/
├── stylesheet/
└── javascript/
```

---

## Step 2 — Activate the theme

Open `C:\laragon\www\opencart\config.php` and find:

```php
define('DEFAULT_THEME', 'default');
```

Change it to:

```php
define('DEFAULT_THEME', 'mytheme');
```

---

## Step 3 — Overriding Templates

To override a template from the default theme:

1. Find the file inside `catalog/view/theme/default/template/`
2. Copy it to the **same relative path** inside `mytheme/template/`
3. Make your changes

**Example:**
```
default: catalog/view/theme/default/template/common/header.twig
mytheme: catalog/view/theme/mytheme/template/common/header.twig
```

> OpenCart automatically loads the file from `mytheme` if it exists, otherwise falls back to `default`.

---

## Step 4 — Clear the cache

After any template change, clear the OpenCart cache:

1. Go to `http://opencart.test/admin`
2. **Extensions → Modifications → Refresh** (blue button)
3. Or manually delete the contents of:

```
system/storage/cache/
```

---

## Golden Rules

- ✅ Always work inside **mytheme**
- ✅ Only copy files you need to modify
- ✅ Clear cache after every template change
- ❌ Never modify the `default` theme directly
