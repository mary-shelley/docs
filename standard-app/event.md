## Event management

The `event-module` prepare for you an event dispatcher and its depends on `symfony/event-dispatcher`

You can require for `event` in your flow

```php
class IndexController
{
    private $events;
    
    /**
     * @Inject({"event"})
     */
    public function __construct($events)
    {
        $this->events = $events;
    }
    
    /**
     * @Middleware\Route("/signup", methods={"GET"})
     */
    public function indexAction($request, $response)
    {
        $users = $this->events->dispatch('user.signup', new GenericEvent($user, [/*more data*/]));
        ...
    }
}
```

Of course in your module you have to register also listeners

```php
$events->addListener("user.signup", $invokable);
```
