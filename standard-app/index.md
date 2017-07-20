## Standard Application

You can create the standard application (that have multiple dependencies) using composer:

```sh
$ composer create-project wdalmut/frankie-standard-app:dev-master myapp
```

### Modules

The standard application have multiple dependencies

 * [Twig as template engine](twig.html)
 * Doctrine ORM for database connection
 * Zend Mail as SMTP helper
 * Monolog for logging support
 * Whoops for error management
 * Symfony Event Dispatcher for event management
 * Unit testing with PHPUnit
 * Integration/Functional testing with PHPUnit
