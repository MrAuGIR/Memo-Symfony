## methode personalisé

ex :
```
#[
    ApiResources(
        itemOperations: [
            'publish' => [
                'method' => 'POST',
                'path' => '/posts/{id}/publish',
                'controller' => 'PostPublishController::class',
                'openapi_context' => [
                    'summary' => 'Permet de publier un article',
                    'requestBody' => [
                        'content'=>[
                            'application/json' => [
                                'schema' => []
                            ]
                        ]                    
                    ]
                ]
            ]
        ]
    )
]

```
```
// PostPublishController

class PostPublishController
{
    publis function __invoke(Post $data): Post
    {
        //on jaoute notre logique
        return $data;
    }
}
```

2. Open api
documentaton de l'api
#[
    ÀpiProperty(
        openApiContext: ['type'=> 'boolean']

    )
]
private $online = false;

3. point d'entrée non lié à une entité **DataProvider**
4. sauvegarder de nouvelle entité **DataPersister**

