# Fix symfony/intl for newer Php Versions (^7.3.4, ^7.2.17, ^7.1.28)

As mention in https://github.com/symfony/symfony/issues/31089
Symfony can end up in a infinite loop.

A fix for this issue is only provided in Symfony ^3.4.24 and  ^4.2.7

For older Symfony versions you can use this fix. It will overwrite the Locale class
of the Symfony to fix the infinite loop problem.
