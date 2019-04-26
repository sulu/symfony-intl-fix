# Fix symfony/intl for newer PHP Versions

```bash
composer require sulu/symfony-intl-fix
```

To avoid problems you should also exclude default Locale class from the classmap in your `composer.json`:

```json
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

If you use one of the above PHP Version and a older Symfony Intl version than `^3.4.24` or `^4.2.7`
symfony/intl will endup in a infinite loop.

This package will overwrite the Symfony [Locale](https://github.com/symfony/symfony/blob/master/src/Symfony/Component/Intl/Locale.php)
to avoid this infinite loop. Projects using Symfony 3 or 4 should just update there symfony package.
This fix is mainly provided for Symfony 2 projects.

**What was changed to fix the issue?**

The change is really simple in `Locale.php` 

```diff
-            return locale_compose($localeSubTags);
+            $fallback = locale_compose($localeSubTags);
+
+            return false !== $fallback ? $fallback : null;
```

See [original commit](https://github.com/symfony/intl/commit/d2ac83703951bc3206e9ea3f6114b355de14e3ce#diff-272fb631cccddf1d11988bec3fb7aa15).


