

```
$response = new Response()

$rsponse->header->set('content-type', 'text/html; charset=utf-8')
$response->setContent(sprintf('Hello %s', htmlspecialchar(name)))

```