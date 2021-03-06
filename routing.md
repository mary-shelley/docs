## Routing

The routing system is handled by the Symfony Routing component but Frankie uses
annotation in order to define your application routes. The general principle is:

```php
class A
{
    /**
     * @Route("/resource", methods={"POST"})
     */
    public function method(){}
}
```

The framework pass always the request and response to your action and any other
request parameter, look this example:

```php
class A
{
    /**
     * @Route("/")
     */
    public function method(Request $request, Response $response){}
}
```

where Request is an `Symfony\\Component\\HttpFoundation\\Request` and the Response
is an `Symfony\\Component\\HttpFoundation\\Response`

### Parameters

In addition if your route uses parameters, those are passed to your method

```php
class A
{
    /**
     * @Route("/path/{act}/met/{oth}")
     */
    public function method(Request $request, Response $response, $act, $oth){}
}
```

With PHP 5.6 could be interesting apply variadics to actions, like:

```php
class A
{
    /**
     * @Route("/path/{act}/met/{oth}")
     */
    public function method(Request $request, Response $response, ...$params){}
}
```

Or even more

```php
class A
{
    /**
     * @Route("/path/{act}/met/{oth}")
     */
    public function method(...$params)
    {
        //$params[0] <- request
        //$params[1] <- response
        //$params[2] <- act
        //$params[3] <- oth
    }
}
```

But actually seems that we have some problem with annotation parsing, check this
out: https://github.com/symfony/symfony/pull/13690

### More details

Thanks to the symfony router we can add more sugar to our annotations like
requirements

```php
class Book
{
    /**
     * @Route("/book/{id}", methods={"GET"}, requirements={"id"="\d+"})
     */
    public function method(Request $request, Response $response, $id) {}
}
```

### Route prefix

You can use the base class in order to create a default route path


```php
/**
 * @Route("/user")
 */
class UserController
{
    /** @Route("/{id}", methods={"GET"}, requirements={"id"="\d+"}) */
    public function method(Request $request, Response $response, $id) {}
}
```

The resulting action route match: `/user/12` for example
