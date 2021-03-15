# 1 Securisé les routes

### A *IsGranted()* utiliser pour restrindre l'accès à certaine _route_

les imports :
```
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Security;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\IsGranted;
```

exemple :
```
    /**
     * @IsGranted("ROLE_ADMIN")
     *
     * or use @Security for more flexibility:
     *
     * @Security("is_granted('ROLE_ADMIN') and is_granted('ROLE_FRIENDLY_USER')")
     */
    public function index()
    {
        // ...
    }

```
plusieurs "role" autorisé, 
@IsGranted("POST_SHOW", subject="post") est un exemple pour illustré l'utilisation de voters de security personnalisé
```
    /**
    * @Route("/posts/{id}")
    *
    * @IsGranted("ROLE_ADMIN")
    * @IsGranted("POST_SHOW", subject="post")
    */
    public function show(Post $post)
    {
    }

```

```
    /**
    * Will throw a normal AccessDeniedException:
    *
    * @IsGranted("ROLE_ADMIN", message="No access! Get out!")
    *
    * Will throw an HttpException with a 404 status code:
    *
    * @IsGranted("ROLE_ADMIN", statusCode=404, message="Post not found")
    */
    public function show(Post $post)
    {
    }

```

### B en utilisant l'annotation *@Security* qui est plus "flexible"

exemple : 2 roles autorisé
```
    /**
    * @Security("is_granted('ROLE_ADMIN') and is_granted('POST_SHOW', post)")
    */
    public function show(Post $post)
    {
        // ...
    }

```
autre exemple avec personnalisation du code d'exception et du message
```
    /**
    * @Security("is_granted('POST_SHOW', post)", statusCode=404, message="Resource not found.")
    */
    public function show(Post $post)
    {
    }

```