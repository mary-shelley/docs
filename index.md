## Getting Started

Getting started with Frankie is super-simple, you can create the base project
using composer:

```sh
$ composer create-project wdalmut/frankie-tiny-app:dev-master myapp
$ cd myapp
```

Now just bring up your dev server:

```sh
$ php -S localhost:8080 -t web
```

And navigate to: ["http://localhost:8080/"](http://localhost:8080)

### Use the standard application

[The standard application](standard-app) is much more complete than the `tiny-app` because it depends on more pre-definded modules like: Twig, Doctrine, etc. 

### What next?

 * [Routing](routing.html)
 * [Steps (middlewares)](steps.html)
 * [Action shortcuts](shortcuts.html)
 * [Error Handler](errors.html)
 * [Create your own module](modules.html)
 * [Why Frankenstein (as name)?](frankenstein.html)

