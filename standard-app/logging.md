## Log with monolog

You can add you log information just injecting the `logger` instance (using Monolog as logging framework)

```php
class IndexController
{
    private $logger;
    
    /**
     * @Inject({"logger"})
     */
    public function __construct($logger)
    {
        $this->logger = $logger;
    }
    
    /**
     * @Middleware\Route("/", methods={"GET"})
     */
    public function indexAction($request, $response)
    {
        $this->logger->info("Here my log information");
    }
}
```

### Configure your logger adapter

You can change the service configuration to change the logger writer adapter, for example:

```php
new LoggerModule([
    'name' => 'default',
    'handlers' => [
        StreamHandler::class => [
            'path' => '/tmp/test.log',
            'level' => Logger::DEBUG, // filter logs
        ],
    ],
]),
```
