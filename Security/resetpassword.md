## Mise en place du reset password des utilisateurs

``composer require symfonycasts/reset-password-bundle``

``php bin/console make:reset-password``

La commande va demander :
1. quelle route pour les utilisateurs qui vont reinitialiser leur mot de passe avec success. ( ex: app_login)
2. l'adresse email qui va envoyer les messages aux users

Ensuite faire une make:migration
puis une doctrine:migrations:migrate

Ensuite penser a ajouter le lien vers 'app_forgot_password_request' dans le template twig de login