# Fix symfony/intl for newer PHP Versions

```bash
composer require sulu/symfony-intl-fix
```

To avoid problems you should also exclude default Locale class from the classmap in your `composer.json`:

```
{
    "autoload": {
        "exclude-from-classmap": [
             "vendor/symfony/intl/Locale.php",
             "vendor/symfony/symfony/src/Symfony/Component/Intl/Locale.php"
        ]
    }
}
```

**Effected PHP Versions:**

 - `^7.3.4`
 - `^7.2.17`
 - `^7.1.28`

If you use when of the above PHP Version and a older Symfony version than `^3.4.24` or `^4.2.7`
symfony/intl will endup in a infinite loop.

This package will overwrite the Symfony [Locale](https://github.com/symfony/symfony/blob/master/src/Symfony/Component/Intl/Locale.php)
to avoid this infinite loop. Projects using Symfony 3 or 4 should just update there symfony package.
This fix is maily provided for Symfony 2 users.
