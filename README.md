LswApiCallerBundle
==================

The LswApiCallerBundle adds a CURL API caller to your Symfony2 application.
It is easy to use from the code and is aimed to have full debugging capabilities.

## Requirements

* PHP 5.3 with curl support
* Symfony 2.1 (works under Symfony 2.0 as well)

## Installation

Installation is broken down in the following steps:

1. Download LswApiCallerBundle using composer
2. Enable the Bundle
3. Make sure php5-curl is installed (CURL module for php5)

### Step 1: Download LswGettextTranslationBundle using composer

Add LswGettextTranslationBundle in your composer.json:

```js
{
    "require": {
        "leaseweb/gettext-translation-bundle": "*"
    }
}
```

Now tell composer to download the bundle by running the command:

``` bash
$ php composer.phar update leaseweb/gettext-translation-bundle
```

Composer will install the bundle to your project's `vendor/leaseweb` directory.

### Step 2: Enable the bundle

Enable the bundle in the kernel:

``` php
<?php
// app/AppKernel.php

public function registerBundles()
{
    $bundles = array(
        // ...
        new Lsw\GettextTranslationBundle\LswGettextTranslationBundle(),
    );
}
```

### Step 3: Make sure php5-curl is installed

On a Debian based distribution (like Ubuntu) the package is called "php5-curl" and
can be installed using the following commands:

``` bash
$ sudo apt-get install php5-curl
$ sudo service apache2 restart
```

On a RedHat based distribution (like CentOS) the package is called "php-curl" and
can be installed using the following commands:

``` bash
$ sudo yum install php-curl
$ sudo service httpd restart
```

To check this create and run a PHP file with the following contents:

``` php
<?php phpinfo() ?>
```

It should display that the option "cURL support" is set to "enabled".

This package should work on a Windows installation as well provided the CURL support
is enabled in PHP.

## Usage

You can use the caller by getting the service "api_caller" and using the "call" function with one of
the available call types:

- HttpGetJson
- HttpPostJson
- HttpPutJson
- HttpDeleteJson
- HttpGetHtml

Example of usage with the "HttpGetJson" call type:

``` php

use Symfony\Bundle\FrameworkBundle\Controller\Controller
use Lsw\ApiCallerBundle\Call\HttpGetJson;

class SomeController extends Controller
{
    public function someAction()
    { 
        ...
        $output = $this->get('api_caller')->call(new HttpGetJson($url, $parameters));
        ...
    }
}

```
