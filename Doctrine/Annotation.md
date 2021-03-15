# Annotation

###### Penser aux imports
```
use Symfony\Component\Validator\Constraints as Assert;
use Symfony\Bridge\Doctrine\Validator\Constraints\UniqueEntity;
```

###### 1 Propriété unique dans une entité
```
    @UniqueEntity(
    * fields= {"email"},
    * message="l'email est déjà utilisée"
    * )
    class User implements UserInterface
    {
        ...
```