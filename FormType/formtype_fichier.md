
**Ajouter** le ``use Symfony\Component\Validator\Constraints\NotBlank;`` pour la contraint **NoBlank**

```

public function buildForm(FormBuilderInterface $builder, array $options)
    {
        $builder
            ->add('name', TextType::class, [
                'label'=> 'Nom de la catégorie',
                'attr' => ['placeholder' => 'nom de la category',
                           'class'=> 'form-control'],
                'constraints' => [
                    new NotBlank([
                        'message' => 'Le nom de la catégorie est obligatoire',
                    ]),
                ]
            ])
            ->add('color', ColorType::class,[
                'label' => 'Couleur de la catégorie',
                'attr' => ['class'=> 'form-control']
            ])
            ->add('logo', FileType::class, [
                'label' => 'logo',
                'attr' => ['class'=> 'form-control'],
                'mapped' => false,
                'required' => false
            ])
        ;
    }
```