# TwigConstantAccessorBundle

[![Build Status](https://travis-ci.org/jdecool/TwigConstantAccessorBundle.svg?branch=master)](https://travis-ci.org/jdecool/TwigConstantAccessorBundle)

This bundle simplify access of your class constants in Twig.

## Install it

Install extension using [composer](https://getcomposer.org):

```json
{
    "require": {
        "jdecool/twig-constant-accessor-bundle": "~1.0"
    }
}
```

Enable the extension in your application `AppKernel`:

```php
<?php

public function registerBundles()
{
    $bundles = [
        // ...
        new JDecool\Bundle\TwigConstantAccessorBundle\JDecoolTwigConstantAccessorBundle(),
    ];

    // ...

    return $bundles;
}
```

Register the class you want to access constant in your container configuration :

```yaml
services:
    my_service:
        class: Namespace\To\ServiceClass
        tags:
            - { name: twig.constant_accessor }

    my_collection:
        class: MyClass
        tags:
            - { name: twig.constant_accessor, alias: 'MyClassAlias' }
```

After you can access your class constant in your templates :

```twig
{{ ServiceClass.MY_CONSTANT }}
{{ MyClassAlias.KEY }}

{% if 'value' == ServiceClass.My_CONSTANT %}Test is OK{% endif %}
```