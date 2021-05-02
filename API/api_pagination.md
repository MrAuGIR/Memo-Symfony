1. pagination

dans la déclaration apiResource :
```
#ApiResource(
    
    paginationItemsPerPage : 2,
    paginationMaximumItemsPerPage: 2,
    paginationClientItemsPerPage: true
)
```


2. filtre
en dehors de la déclaration apiResource de l'item
```
#[
    apiResources(//les parametres),

    ApiFilter(SearchFilter::class, properties: ['id'=>'exact', 'title'=>'partial'])
]


```
api platform va adpater la requète qui est généré en focntion des filtres créés:
ex : `` https://localhost:8000/api/posts?page=1&itemsPerPage=2&title=second ``