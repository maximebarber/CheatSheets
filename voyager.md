# Voyager

## Table of contents
1. [Installation](#1-installation)
2. [Configuration](#2-configuration)
3. [Routing](3#-routing)

# 1. Installation

* Create new laravel project
> composer create-project laravel/laravel _myapp_
* > composer require tcg/voyager
* Modify .env if neccessary
> php artisan voyager:install (--with-dummy)
* Create new admin
> php artisan voyager:admin your@email.com --create
* Visit and login at /admin

# 2. Configuration

* Go to voyager.php

# 3. Routing

Change admin prefix
* Modify web.php
* voyager.php

