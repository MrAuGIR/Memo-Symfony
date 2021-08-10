### Pour pouvoir installer un service et beneficier de l'injection de dépendance en plus
### il faut modifier le fichier services.yaml

**exemple avec la librairie slugify, installer via composer

```
    //dans le fichier services.yaml
    Cocur\Slugify\Slugify: ~ 
```

### De cette façon le conteneur de service apprend que le service slugify existe et ensuite on peut beneficier de l'autowiring

**de cette façon**
```
class HelloController
{
    protected $logger;
    protected $calculator;

    /**
     * @Route("/hello/{name?World}", name="hello")
     */
    public function hello(Slugify $slug)
    {
        dump($slug->slugify("hello world"));
        
    }

}

```

si on fait un `` php bin/console debug:autowiring --all`` le service apparait

## dans le cas des bundles, symfony va automatiquement rajouter les services au conteneurs de service
les bundles ajouter apparaissent dans bundles.php, ce qui permet a symfony de faire connaitres au conteneurs de services les nouveaux services (nouvelles classes).

