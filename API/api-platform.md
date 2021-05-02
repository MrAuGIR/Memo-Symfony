# API PLATFORM

lien utile :
https://api-platform.com/docs/distribution/#using-symfony-and-composer

#### CREATION DU PROJET
`` composer create-project symfony/skeleton tuto-api ``

### API platform component
`` composer require api ``

### Base de donnée et schema
`` php bin/console doctrine:database:create ``
``php bin/console doctrine:schema:create ``

##### creation d'une ressource
1. ``composer require symfony/maker-bundle --dev ``

2. `` php bin/console make:entity ``

##### format
1. entête application ld+json
   on recupère des données en plus, ce sont des attribut hydra->information sur l'opération en cours
   (page suivant, precedente, nombre d'item dans le cas d'une pagination) utilisable ensuite par notre front

### Fonctionnement api-platform

requête -> intercepte par api platform et regarde si c'est quelque chose qu'il connait
si oui il va recupéré les donnée avec l'orm doctrine au travers des class dataProvider