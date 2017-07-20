## Use Twig Module

You can prepare your controllers with the `Twig` dependency and use it to serialize a template

```php
class IndexController
{
    /**
     * @Inject({"twig"})
     */
    public function __construct($twig)
    {
        $this->twig = $twig;
    }
    
    /**
     * @Middleware\Route("/", methods={"GET"})
     */
    public function indexAction($request, $response)
    {
        // Set the right content-type header
        $response->headers->set("Content-Type", "text/html");
        
        // Convert the twig template to an page HTML
        $response->setContent(
           $this->twig->render('index/index.html.twig', ["to" => "World"]);
        );
        
        return $response;
    }
}
```

Of couse you can wrap the serialization process to a separate step and use it as `@After` step

```php
/**
 * @Middleware\Route("/", methods={"GET"})
 * @Middleware\After(targetClass="App\Serializer", targetMethod="asHtml")
 */
public function indexAction($request, $response)
{
    return $this->twig->render('index/index.html.twig', ["to" => "World"]);
}
```
