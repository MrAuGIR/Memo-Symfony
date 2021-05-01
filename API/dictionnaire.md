###### normalizationContext (object -> array -> json) gère qui va normaliser les objets
1. Définir les champs de vos entités qui vont être convertie au travers de vos groupe de normalisation.
   
###### denormalizationContext (json -> array -> object) ce qui est reçu dans les requête et transférer dans l’objet final

__exemple__
```
#[ApiResource(
    denormalizationContext: ['groups' => ['write:Post']],
    normalizationContext: [
        'groups' => ['read:collection'],
        'openapi_definition_name' => 'Collection'
    ]
)]
```

###### itemOperations :  opérations spécifiques disponibles au niveau des items,
1. on peut pour chaque opération (get, put, post,…) créer des contexte de normalization/denormailzation specifiques à un item (exemple rajouter un groupe de normalisation en plus de celui par defaut dans noramilzationContext)

```
itemOperations: [
        'put',
        'delete',
        'patch',
        'get' => [
            'normalization_context' => [
                'groups' => ['read:collection', 'read:item', 'read:Post'],
                'openapi_definition_name' => 'Detail'
            ]
        ],
```
   
###### collectionOperations: opérations disponibles au niveau des collections
