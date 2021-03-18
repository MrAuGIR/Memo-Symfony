

1. création du projet `` composer create-project symfony/website-skeleton <nom-du-projet> `` ou `` symfony new --full <nom-du-projet>``

2. création de la class security user `` php bin/console make:user `` (elle implemente UserInterface)

3. mise a jour de la class user `` php bin/console make:entity User`` (on rajoute des champs ou des relations)

4. création de la base de donnée `` php bin/console doctrine:database:create ``

5. creation du fichier de migration `` php bin/console make:migration ``

6. Creation du système de login ``php bin/console make:auth``

7. Modification du chemin du logout dans la fonction de la class créé

8. formulaire d'enregistrement : ``php bin/console make:registration-form``
    1. Possible warning si **symfonycasts/verify-email-bundle** non installé et option d'email selectionné
    2. bonne pratique de logguer les users après l'enregistrement
    3. Attention après la mise en place du controller de registration, il y a des configuration a faire, exemple: redirectroute dans __verifyUserEmail()__ dans __registrationController__.
    4. faire fichier migrate et doctrine migration

9. Mise en place de fixture  :
    1. composer bundle fixtures : `` composer require --dev doctrine/doctrine-fixtures-bundle ``
    2. composer librairie faker : `` composer require --dev fakerphp/faker ``
    3. option ajouter un bibliothèque d'image pour fake : ```composer require --dev bluemmb/faker-picsum-photos-provider ``
    ```
        use bluemmb\Faker\PicsumPhotosProvider;

        $faker = Factory::create('fr_FR')
        $faker->addProvider(new \Bluemmb\Faker\PicsumPhotosProvider($faker))
    ```
    4. Lancer les fixtures : `` php bin/console doctrine:fixtures:load ``
    
10. Definir les routes et les controllers

11. Premier controlleur ``php bin/console make:controller main``


