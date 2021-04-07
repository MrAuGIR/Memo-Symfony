
Lien utile : https://symfony.com/doc/current/frontend/encore/bootstrap.html

### Dans le terminal :
 1. `` composer require symfony/webpack-encore-bundle ``
 2. `` yarn install``
 3. decommenter les lignes dans __base.html.twig__
    ```
    {# templates/base.html.twig #}
    <!DOCTYPE html>
    <html>
        <head>
            <!-- ... -->

            {% block stylesheets %}
                {# 'app' must match the first argument to addEntry() in webpack.config.js #}
                {{ encore_entry_link_tags('app') }}

                <!-- Renders a link tag (if your module requires any CSS)
                    <link rel="stylesheet" href="/build/app.css"> -->
            {% endblock %}

            {% block javascripts %}
                {{ encore_entry_script_tags('app') }}

                <!-- Renders app.js & a webpack runtime.js file
                    <script src="/build/runtime.js" defer></script>
                    <script src="/build/app.js" defer></script>
                    See note below about the "defer" attribute -->
            {% endblock %}
        </head>

        <!-- ... -->
    </html>
    ```
 4. lancer le serveur de developpement : `` yarn encore dev-server ``
 5. pensé a run le builder : 

### Utilisation de yarn :
1. compiler les assets (manuel) (mode dev)
        ``yarn encore dev``
2. compiler les assets automatiquement (watcher)
        ``yarn encore dev --watch``
3. passer les asset en prod
        ``yarn encore production``


### Installer bootstrap dans son application symfony (si on travail en scss)
1. `` yarn add bootstrap --dev ``
2.  le boostrap est maintenant dans le dossier *nodes_modules*
On peut l'importer dans un fichier scss par exemple _global.scss_ ou  renommer le fichier _app.css_ en _app.scss_

```
// assets/styles/app.scss

// the ~ allows you to reference things in node_modules
@import "~bootstrap/scss/bootstrap";

```

3. decommenter le scass loader dans le fichier webpack.config.js
```
// enables Sass/SCSS support
//.enableSassLoader()
```
4. installer le yarn sassloader
   `` yarn add sass-loader@^11.0.0 sass --dev ``

5. ajouter le javascript de bootstrap
   `` yarn add jquery popper.js --dev ``

6. lancer la compilation en manuelle ou en automatique


7. Mettre en ligne
   1. soit installer node puis yarn et ensuite lancé la compilation
   2. soit build en local `` yarn run encore production ``
   et copier le fichier /public/build en local dans le dossier public de l'hebergement