#Exemple

###### Formulaire type avec double champs de mot de passe

```

    public function buildForm(FormBuilderInterface $builder, array $options)
    {
        $builder
            ->add('email', EmailType::class, [
                'label' => 'votre email',
                'attr' => ['class' => 'form-control'],
                'mapped' =>false
            ])
            ->add('lastName', TextType::class,[
                'label' => 'Votre nom',
                'attr' => ['class' => 'form-control'],
            ])
            ->add('firstName', TextType::class,[
                'label' => 'Votre prénom',
                'attr' => ['class' => 'form-control']
            ])
            ->add('agreeTerms', CheckboxType::class, [
                'mapped' => false,
                'constraints' => [
                    new IsTrue([
                        'message' => 'Vous devez accepter les conditions générals d\'utilisation',
                    ]),
                ],
            ])
            ->add('plainPassword', RepeatedType::class, [
                'options' => ['attr' => ['class' => 'form-control']],
                'type' => PasswordType::class,
                'mapped' => false,
                'invalid_message' => 'les mots de passes doivent être identique',
                'first_options'   => array('label' => 'Password'),
                'second_options'  => array('label' => 'Repeat Password'),
                'constraints' => [
                    new NotBlank([
                        'message' => 'Veuillez saisir un mot de passe',
                    ]),
                    new Length([
                        'min' => 6,
                        'minMessage' => 'Your password should be at least {{ limit }} characters',
                        // max length allowed by Symfony for security reasons
                        'max' => 4096,
                    ]),
                ],
            ])
        ;
    }
```