# FormType


###### builder avec select

```
    public function buildForm(FormBuilderInterface $builder, array $options)
    {
        $builder
            ->add('email')
            ->add('roles',ChoiceType::class,[
                'choices' => [
                    'Administrateur' => 'ROLE_ADMIN',
                    'Editeur' => 'ROLE_USER'
                ],
                'mapped' => false
            ])
            ->add('password', PasswordType::class)
        ;
    }
```