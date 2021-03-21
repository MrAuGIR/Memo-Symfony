# Validator

On peut ajouter des contraintes sur les champs d'une entité soit on passant par le fichier entité avec l'ajout d'annotation,
soit une seconde approche en ajoutant ces contraintes au(x) formulaire type de l'entité.

**lien utile** :
    1.  https://symfony.com/doc/current/forms.html#processing-forms

    2. https://symfony.com/doc/current/validation.html



1. ###### Exemple d'utilisation des composants de validations dans les entités
   ```
    // src/Entity/Article.php
    namespace App\Entity;

    use Symfony\Component\Validator\Constraints as Assert;

    class Article
    {
        /**
        * @Assert\NotBlank
        */
        public $title;

        /**
        * @Assert\NotBlank
        * @Assert\Type("\DateTime")
        */
        protected $createdAt;
    }
    ```
2. `` use Symfony\Component\Validator\Constraints as Assert; `` a rajouter dans les fichiers entités

3. ### Message de validation de formulaire (en cas d'erreur ?) - Introduit avec symfony 5.2
 ```
    # config/packages/framework.yaml
    framework:
        form:
            legacy_error_messages: false

 ```

 4. #### Utiliser la validation 
 ajouter la ligne suivantes au fichier  *config/packages/framework.yaml*
 
```
framework:
    validation: { enabled: true }
```

5. Contraintes sur les champs des formulaire
```
public function buildForm(FormBuilderInterface $builder, array $options)
{
    $builder
        ->add('myField', TextType::class, [
            'required' => true,
            'constraints' => [new Length(['min' => 3])],
        ])
    ;
}
```