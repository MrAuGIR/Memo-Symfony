

1. création du projet `` composer create-project symfony/website-skeleton <nom-du-projet> ``
2. création de la class security user `` php bin/console make:user `` (elle implemente UserInterface)
3. mise a jour de la class user `` php bin/console make:entity User`` (on rajoute des champs ou des relations)
4. création de la base de donnée `` php bin/console doctrine:database:create ``
5. creation du fichier de migration `` php bin/console make:migration ``
6. 