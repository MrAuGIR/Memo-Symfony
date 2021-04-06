# Les requètes

**lien utile**: https://symfony.com/doc/current/forms.html


```
request: equivalent of $_POST;
query: equivalent of $_GET ($request->query->get('name'));
cookies: equivalent of $_COOKIE;
attributes: no equivalent - used by your app to store other data (see below);
files: equivalent of $_FILES;
server: equivalent of $_SERVER;
headers: mostly equivalent to a subset of $_SERVER ($request->headers->get('User-Agent')).
```

### exemple 
recupération des données passé en post
```
    if($request->isMethod('POST'))
    {
        $name = $request->request->get('name')
    }
```

recuperation d'un get avec valeur par defaut si nul

``name = $request->query->get('name','toto')``


### form many to many
1. dans le controller 
```

public function addArticle(Request $request):Response
{
    $article = new Article()
    $form = $this->createForm(Article::class, $article);

    $form->handleRequest($request);

    if($form->isSubmitted() & $form->isValid())
    {
        $em = $this->getDoctrine()->getManager();
        $em->persist($article);
        $em->flush();

        return $this->redirectToRoute('article');
    }

    return $this->return('article/ajout.html.twig, [
        'form' => $form->createView()
    ])
}


```