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