

1. création du projet `` composer create-project symfony/website-skeleton <nom-du-projet> `` ou `` symfony new --full <nom-du-projet>``
   1. ou en installant une version définie:
      1. `` composer create-project symfony/website-skeleton:"5.1.*" test4 ``
      2. `` symfony new --full --version=5.2 <nom-du-projet> ``

2. création de la class security user `` php bin/console make:user `` (elle implemente UserInterface)

3. mise a jour de la class user `` php bin/console make:entity User`` (on rajoute des champs ou des relations)

4. création de la base de donnée `` php bin/console doctrine:database:create ``

5. creation du fichier de migration `` php bin/console make:migration ``

6. Creation du système de login ``php bin/console make:auth``

7. Modification du chemin du logout dans la fonction de la class créé

8. formulaire d'enregistrement : ``php bin/console make:registration-form``
    1. Possible warning si **symfonycasts/verify-email-bundle** non installé et option d'email selectionné
        ``composer require symfonycasts/verify-email-bundle``
    2. bonne pratique de logguer les users après l'enregistrement
    3. Attention après la mise en place du controller de registration, il y a des configuration a faire, exemple: redirectroute dans __verifyUserEmail()__ dans __registrationController__.
    4. faire fichier migrate et doctrine migration
    5. penser a modifier le controller pour l'enregistrement des users pour enregistrer les donners du user avant le flush()
    6. avoir créé un controller main (pour la redirection vers la home)

9.  Oublie mot de passe :
    
    `` composer require symfonycasts/reset-password-bundle ``
    `` php bin/console make:reset-password ``
    
    1. La commande va demander :
        1. quelle route pour les utilisateurs qui vont reinitialiser leur mot de passe avec success. ( ex: app_login)
        2. l'adresse email qui va envoyer les messages aux users

    2. Ensuite :
       1. Run ``php bin/console make:migration`` to generate a migration for the new "App\Entity\ResetPasswordRequest" entity.
       2. Review forms in "src/Form" to customize validation and labels.
       3. Review and customize the templates in ``templates/reset_password``.
       4. Make sure your MAILER_DSN env var has the correct settings.
       5. Create a "forgot your password link" to the app_forgot_password_request route on your login form.
s
10. Mise en places des autres entity 
    ``php bin/console make:entity ``
    ou
    ``symfony console make:entity``

11. Mise en place de fixture  :
    1. composer bundle fixtures : `` composer require --dev doctrine/doctrine-fixtures-bundle ``
    2. composer librairie faker : `` composer require --dev fakerphp/faker ``
    3. option ajouter un bibliothèque d'image pour fake : ``composer require --dev bluemmb/faker-picsum-photos-provider ``
    ```
        use bluemmb\Faker\PicsumPhotosProvider;

        $faker = Factory::create('fr_FR')
        $faker->addProvider(new \Bluemmb\Faker\PicsumPhotosProvider($faker))
    ```
    1. Lancer les fixtures : `` php bin/console doctrine:fixtures:load ``

12. Definir les routes et les controllers

13. Premier controlleur ``php bin/console make:controller main``

14. Réaliser une interface d'administration
    lien utile : https://nouvelle-techno.fr/actualites/6-creer-une-interface-dadministration-avec-symfony-5-1-sans-bundle

    1.  Créé un __AdminController__ et le placer dans un dossier admin */src/controller/Admin*
    2.  modifier le namespace du fichier en *namespace App\Controller\Admin*
    3.  Dans le fichier *security.yaml* : 
    ```
        # Easy way to control access for large sections of your site
        # Note: Only the *first* access control that matches will be used
        access_control:
            - { path: ^/admin, roles: ROLE_ADMIN }
    ```
    pour ne permettre que les utilisateurs authentifié avec le level admin à acceder à cette route

    4. Séparer les controller pour chaque entité (utilisation de l'annotation @package)
    5. Créer le crud d'une entité `` php bin/console make:crud `` (idem deplacer dans le dossier **Admin** en modifiant le mot de passe)

15. Profil utilisateur
    1.  Créer un formulaire type pour modifier le mot de passe ou le faire en dure dans twig
    `` php bin/console make:form ``

