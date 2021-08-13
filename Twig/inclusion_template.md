soure : https://twig.symfony.com/doc/3.x/templates.html#including-other-templates

**le controlleur**
```
    public function hello(Environment $twig)
    {
        
        $html = $twig->render('hello.html.twig',[
            'formateur' => [
                'prenom' => 'lior',
                'nom'=> 'chamlat',
                'age' => 33
            ],
            'formateur2' => [
                'prenom' => 'jean',
                'nom'=> 'dupont',
                'age' => 33
            ]
        ]
        );
        return new Response($html);
    }
```


**le template à inclure** _formateur.html.twig

```
  <p>
    <strong>{{formateur.prenom}}</strong>
    {{formateur.nom}}
 </p>
```


**le template de la page**

```
  {% extends "base.html.twig" %}
    {% block body %}
      {% include "_formateur.html.twig" with {"formateur": formateur1} %}
      {% include "_formateur.html.twig" with {"formateur": formateur2} %}
  {% endblock %}
```

