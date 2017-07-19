## Modules

Frankie modules are just Depedency Injection Containers that are wrapped together using a single `facade` ([container acclimate](https://github.com/AcclimateContainer/acclimate-container)). 

### Create a module

Require `wdalmut/frankie-modular` as a module dependency

```sh
composer require wdalmut/frankie-modular:dev-master
```

You have just to create a class definition that implements a single interface `Corley\Modular\Module\ModuleInterface`

```php
class MyModule implements ModuleInterface
{
    public function getContainer()
    {
        return /* Psr\Container\ContainerInterface instance */
    }
}
```

You can choose your own real container system like: Zend Service Manager, Symfony Dependency Injection Container
but it should implements the PSR-11 interface `Psr\ContainerInterface`.

#### Zend Framework Container example


```php
class MyModule implements ModuleInterface
{
  public function getContainer()
  {
      $serviceManager = new ServiceManager();
      $serviceManager->configure([
        "factories" => [
          "hello" => function($sm) {
            return new \stdClass();
          },
        ]
      ]);
      return $serviceManager
  }
}
```

#### Symfony DiC example

```php

class MyModule implements ModuleInterface
{
  public function getContainer()
  {
    $sfContainer = new DicBuilder();
    
    $loader = new XmlFileLoader($sfContainer, new FileLocator(realpath(__DIR__  . '/../configs')));
    $loader->load(realpath(__DIR__ . '/../configs/services.xml'));
    
    return $sfContainer;
  }
}
```
