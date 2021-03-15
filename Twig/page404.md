# Personnaliser une page 404 pour son application Symfony
lien utile : https://nouvelle-techno.fr/actualites/live-coding-creer-des-pages-derreur-personnalisees-avec-symfony
_installer le packatage suivant_
```
 composer require symfony/twig-pack
```

###### 1 Créer un dossier Exception
```
templates/bundles/TwigBundle/Exception/
```

######  2 Contentant les fichiers twig suivant :
```
templates/
└─ bundles/
   └─ TwigBundle/
      └─ Exception/
         ├─ error404.html.twig
         ├─ error403.html.twig
         └─ error.html.twig      # All other HTML errors (including 500)

```

###### 3 Template twig error404.html.twig
```
{% extends 'base.html.twig' %}

{% block title %}Page non trouvée{% endblock %}

{% block body %}
    <h1>Page non trouvée</h1>
    <p>La page que vous cherchez n'a pas été trouvée</p>
    <p>Le code est : {{status_code}}</p>
    <p>Le texte est : {{status_text}}</p>
{% endblock %}

```

###### 4 Tester la page
```
https://localhost:8000/index.php/_error/404

```