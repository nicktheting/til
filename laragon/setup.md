# Laragon — Local Development Setup

## What is Laragon

Laragon is a lightweight, portable local development environment for Windows. It supports multiple PHP versions, automatic virtual hosts, SSL, and comes with Apache, Nginx, MySQL, Node.js and more.

---

## Installation

1. Download **Laragon Full** from https://laragon.org/download
2. Run the installer as **Administrator**
3. Default path: `C:\laragon`
4. Enable: ✅ Auto start on system start
5. Enable: ✅ Auto create virtual hosts

---

## Folder Structure

```
C:\laragon\
├── bin\
│   ├── php\        ← PHP versions
│   ├── apache\     ← Apache
│   ├── mysql\      ← MySQL
│   └── nginx\      ← Nginx
├── www\            ← Your projects go here
│   ├── opencart\   → http://opencart.test
│   └── wordpress\  → http://wordpress.test
└── tmp\
```

---

## Virtual Hosts

Laragon automatically creates a virtual host for every folder inside `www\`:

```
C:\laragon\www\myproject\ → http://myproject.test
```

After adding a new folder: **Right click tray → Reload**

---

## Switching PHP Versions

Right click tray → **PHP → Switch version**

To add a new PHP version:
1. Download the zip from https://windows.php.net/download
2. Extract to `C:\laragon\bin\php\php-8.x.x\`
3. Restart Laragon

---

## Xdebug Setup

1. Download the correct `.dll` from https://xdebug.org/wizard
2. Copy it to `C:\laragon\bin\php\php-8.x.x\ext\`
3. Add to `php.ini` (Right click tray → PHP → php.ini):

```ini
[xdebug]
zend_extension=xdebug
xdebug.mode=debug
xdebug.start_with_request=yes
xdebug.client_host=127.0.0.1
xdebug.client_port=9003
xdebug.idekey=VSCODE
```

4. Restart Laragon
5. In VS Code install **PHP Debug** extension
6. Add to `.vscode/launch.json`:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "listen",
            "port": 9003
        }
    ]
}
```

---

## Database

- **phpMyAdmin:** Right click tray → Database → phpMyAdmin
- **HeidiSQL:** Right click tray → Database → HeidiSQL
- Default credentials: user `root`, password *(empty)*

---

## Useful Commands (Terminal)

```bash
# Open terminal
Right click tray → Terminal

# Open project in VS Code
cd C:\laragon\www\myproject
code .
```

---

## Golden Rules

- ✅ Keep projects inside `C:\laragon\www\`
- ✅ Use `.test` domains for local development
- ✅ Switch PHP version per project as needed
- ✅ Always run Laragon as Administrator
