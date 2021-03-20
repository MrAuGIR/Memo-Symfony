### Filtres Twig


# intépréter html contenu dans une variable
``raw``

# limité le nombre de caractère d'un string à l'affichage
``<td>{{ article.content | raw | striptags|slice(0, 10) }}</td>``