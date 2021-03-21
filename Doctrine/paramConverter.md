# Param converter
lien utile : https://symfony.com/doc/current/bundles/SensioFrameworkExtraBundle/annotations/converters.html

le use :
    `` use Sensio\Bundle\FrameworkExtraBundle\Configuration\ParamConverter; ``

###### Les annotations paramConverter permettent de convertir les requètes reçu en objet
1 - cas standart
```
    /**
    * recupère le post grace a l'id present dans la route
    *
    * @Route("/blog/{id}")
    */
    public function showByPk(Post $post)
    {
    }

    /**
    * Utilise findOneBy() avec le critère {slug}.
    *
    * @Route("/blog/{slug}")
    */
    public function show(Post $post)
    {
    }

```

2 - va chercher selon un expression
```
    /**
    * @Route("/blog/{post_id}")
    * @Entity("post", expr="repository.find(post_id)")
    */
    public function show(Post $post)
    {
    }

```

3- Les expression peuvent être utiliser pour recupérer plusieurs objects en paramètres
```
    /**
    * @Route("/blog/{id}/comments/{comment_id}")
    * @Entity("comment", expr="repository.find(comment_id)")
    */
    public function show(Post $post, Comment $comment)
    {
    }

```


### les optiosn de paramConverter
indiquer le lien entre l'id du post et le post_id en paramètre de la route
```
    /**
    * @Route("/blog/{post_id}")
    * @ParamConverter("post", options={"id" = "post_id"})
    */
    public function showPost(Post $post)
    {
    }

```

###### mapping
lie les paramètres de la route avec les proprietés des entités
```
    /**
    * @Route("/blog/{date}/{slug}/comments/{comment_slug}")
    * @ParamConverter("post", options={"mapping": {"date": "date", "slug": "slug"}})
    * @ParamConverter("comment", options={"mapping": {"comment_slug": "slug"}})
    */
    public function showComment(Post $post, Comment $comment)
    {
    }

```

###### datetime converter
```
    /**
    * @Route("/blog/archive/{start}/{end}")
    * @ParamConverter("start", options={"format": "!Y-m-d"})
    * @ParamConverter("end", options={"format": "!Y-m-d"})
    */
    public function archive(\DateTime $start, \DateTime $end)
    {

```
ou 
```
    /**
    * @Route("/blog/archive/{start}/{end}")
    */
    public function archive(\DateTime $start, \DateTime $end)
    {
    }

```