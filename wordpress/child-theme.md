# WordPress — Child Theme

## What is a Child Theme

A child theme inherits all the functionality and styling of the parent theme, allowing you to make modifications **without touching** the parent's core files. This means parent theme updates will never overwrite your customizations.

---

## Folder Structure

```
wp-content/
└── themes/
    ├── twentytwentyfive/          ← Parent theme (never touch this)
    └── twentytwentyfive-child/    ← Child theme (work here)
        ├── style.css              ← Required
        ├── functions.php          ← Required
        ├── templates/             ← Custom templates (optional)
        ├── parts/                 ← Template parts (optional)
        └── assets/
            ├── css/
            ├── js/
            └── images/
```

---

## Step 1 — Create the folder

```
wp-content/themes/twentytwentyfive-child
```

---

## Step 2 — style.css

Create `style.css` with the theme header:

```css
/*
Theme Name: Twenty Twenty-Five Child
Template: twentytwentyfive
Version: 1.0.0
Author: Your Name
Description: Child theme of Twenty Twenty-Five
*/
```

> **Important:** The `Template:` value must match **exactly** the folder name of the parent theme.

---

## Step 3 — functions.php

Create `functions.php` to enqueue the stylesheets:

```php
<?php
add_action('wp_enqueue_scripts', function() {
    wp_enqueue_style(
        'parent-style',
        get_template_directory_uri() . '/style.css'
    );
    wp_enqueue_style(
        'child-style',
        get_stylesheet_directory_uri() . '/style.css',
        ['parent-style']
    );
});
```

---

## Step 4 — Activation

1. Go to `http://wordpress.test/wp-admin`
2. **Appearance → Themes**
3. Click **Activate** on the child theme

---

## Step 5 — Overriding Templates

To override a template from the parent theme:

1. Find the file in the parent theme folder
2. Copy it to the **same relative path** inside the child theme
3. Make your changes

**Example:**
```
parent: twentytwentyfive/templates/page.html
child:  twentytwentyfive-child/templates/page.html
```

> WordPress automatically loads the child theme file if it exists, otherwise falls back to the parent.

---

## Golden Rules

- ✅ Always work inside the **child theme**
- ✅ Only copy files you need to modify
- ❌ Never modify the parent theme directly
