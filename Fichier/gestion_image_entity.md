## Cas d'une image/logo lié à une entité

#### Exemple catégorie avec un logo


1.Dans le FormType lié a l'entité catégory
   1. ```
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
2. Dans le controller et dans la méthode create à la soumission du formulaire
    ```
        $logo = $form->get('logo')->getData();
            if($logo != null){
                //on genere un nouveau nom de fichier (codé) et on rajoute son extension
                $fichier = md5(uniqid()) . '.' . $logo->guessExtension();

                // on copie le fichier dans le dossier uploads
                // 2 params (destination, fichier)
                $logo->move($this->getParameter('logo_directory'), $fichier);

                /* Penser a supprimer les ancien fichiers  */
                unlink($this->getParameter('logo_directory') . '/' . $category->getLogo()); //ici je supprime le fichier

                // on stock l'image dans la bdd (son nom)
                $category->setLogo($fichier);
            }


    ```
3. Dans le fichier **services.yaml**
   1. ajouter la ligne suivante pour indiquer on "déposer" les fichiers uploader
   ```
    parameters:
        logo_directory: '%kernel.project_dir%/public/logo'
   ```

4. en plus
   1. afficher l'image dans la table des catgéories
   `` <td><img src="{{asset('logo/' ~ category.logo)}}" alt="logo"></td> ``