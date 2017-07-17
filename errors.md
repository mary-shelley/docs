## Handling Errors

Frankie can't react to 404 pages (no routes) because there is no action to analyze and
preapare and also for any 500 errors (other exceptions).

For that reason the app expose a method in order to register a callable for this
kind of situations.

```php
// web/index.php
$app->setErrorHandler(function(Request $request, Response $response, $e) {
    $response->setContent($e->getMessage());
});
```

The `setErrorHandler` method allows any callable type, for example:

```php
class JsonErrorHandler
{
    public function __invoke(Request $request, Response $response, Exception $e) {
        $response->setStatusCode(500);
        $response->setContent(json_encode(
            [
                "error" => [
                    "message" => $e->getMessage(),
                    "stacktrace" => $e->getTraceAsString(),
                ],
            ]
        );
    }
}
```

The best way to deal with the error handler is registering a `error_handler` in
your dependencies (replace the default `ErrorModule` in your modules list).

Here an example with `ZF2 Service Manager`

```php
use Pimple\Container;
use Corley\Modular\Module\ModuleInterface;

class MyErrorModule implements ModuleInterface
{
    public function getContainer()
    {
        $container = new ServiceManager();
        $continer->configure([
            "factories" => [
                "error_handler" => function($c) {
                    return new JsonErrorHandler();
                }
            ]
        ]);

        return $container;
    }
}
```

that conceptually works as:

```php
class MyErrorModule implements ModuleInterface
{
    public function getContainer()
    {
        $container = new ServiceManager();
        $container->configure([
            "factories" => [
                "error_handler" => function($c) {
                    return function($rq, $rs, $e) {
                        echo $e->getMessage();
                    };
                }
            ]
        ]);

        return $container;

    }
}
```

That's it!

