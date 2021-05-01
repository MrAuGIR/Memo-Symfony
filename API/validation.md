on peut directement créer des groupes de validation directement au niveau de la difinition de votre apiResources
noatemment dans des *collectionOperations* ou *itemOperations*

1. groupe de validation sur collection
**exemple** :
```
dans la definition de l'apiResources :

collectionOperations: [
    'get',
    'post'=> [
        'validation_groups' => ['create:Post']
    ]
]

et sur le champs :

#[
    Length(min: 5, groups: ['create:Post])
]
private $title

```
2. fonction static

```
dans la definition de l'apiResources :

collectionOperations: [
    'get',
    'post'=> [
        'validation_groups' => [Post::class, 'validationGroups']
    ]
]


public static function validationGroups(self $post){
    
    return ['create:Post'];

}
```
3. validation sur item

```


```

**important** en cas de modifcation 
dans les annotation `` cascade="persist" ``