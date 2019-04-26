# Fix symfony/intl for newer PHP Versions

```bash
composer require sulu/symfony-intl-fix
```

To avoid problems you should also exclude the default Locale class from the classmap in your `composer.json`:

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

**Affected PHP Versions:**

 - `^7.3.4`
 - `^7.2.17`
 - `^7.1.28`

If you use one of the above PHP Version and an older Symfony Intl version than
`^3.4.24` or `^4.2.7` symfony/intl will end up in an infinite loop.

This package will overwrite the Symfony [Locale][locale] to avoid this infinite 
loop. Projects using Symfony 3 or 4 should just update there symfony package. 
This fix is mainly provided for Symfony 2 projects.

**What was changed to fix the issue?**

The change in `Locale.php` is really simple:

```diff
-            return locale_compose($localeSubTags);
+            $fallback = locale_compose($localeSubTags);
+
+            return false !== $fallback ? $fallback : null;
```

See [original commit][oc].

[locale]: https://github.com/symfony/symfony/blob/master/src/Symfony/Component/Intl/Locale.php
[oc]: https://github.com/symfony/intl/commit/d2ac83703951bc3206e9ea3f6114b355de14e3ce#diff-272fb631cccddf1d11988bec3fb7aa15
