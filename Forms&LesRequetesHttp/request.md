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