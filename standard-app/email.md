## Send emails with SMTP

The module depends on `Zend\Mail` component. You just require for `smtp` dependency

```php
class IndexController
{
    private $smtp;
    
    /**
     * @Inject({"smtp"})
     */
    public function __construct($smtp)
    {
        $this->smtp = $smtp;
    }
    
    /**
     * @Middleware\Route("/", methods={"GET"})
     */
    public function indexAction($request, $response)
    {
        $mail = new \Zend\Mail\Message();
        $mail->setBody('This is the text of the email.');
        $mail->setFrom('info@mydomain.tld', "Sender's name");
        $mail->addTo('you@yourdomain.tld', 'Name of recipient');
        $mail->setSubject('TestSubject');

        $this->smtp->send($mail);
    }
}
```

You can change transport layers using the service configuration

```php
new SmtpModule([
    'type' => Sendmail::class,
    'options' => [],
]),
```
