## Doctrine ORM

Doctrine ORM is used to connect with database

Create a simple entity

```php
//src/Entity/User.php

/**
 * @ORM\Entity(repositoryClass="App\Entity\UserRepository")
 * @ORM\Table(
 *   name="users",
 *   indexes={
 *     @ORM\Index(name="username_idx", columns={"username"})
 *   }
 * )
 */
class User
{
    /**
     * @ORM\Id
     * @ORM\Column(type="integer", nullable=false)
     */
    private $id;
    
    /**
     *@ORM\Column(type="string", length=35, unique=true)
     */
    private $username;

    /**
     * @ORM\Column(type="string", length=255)
     */
    private $password;
}
```

And use the console to generate entities

```sh
$ ./vendor/bin/doctrine orm:generate-entities src
```

And generate your database schema

```sh
$ ./vendor/bin/doctrine orm:schema-tool:create
```

### Doctrine as dependency

In your controller you can inject the entity manager to use the doctrine as dependency

```php
class IndexController
{
    private $entityManagaer;
    
    /**
     * @Inject({"orm"})
     */
    public function __construct($entityManager)
    {
        $this->entityManager = $entityManager;
    }
    
    /**
     * @Middleware\Route("/user", methods={"GET"})
     */
    public function indexAction($request, $response)
    {
        $users = $this->entityManager->getRepository("App\Entity\User")->findAll();
        
        // work with all users
        ...
    }
}
```
