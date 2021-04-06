## FormType avec select lié a une relation entre entité

###### exemple avec un choix de Catégorie pour un article
```
            //Form/ArticleType.php

            ->add('category',EntityType::class,[
                'label' => 'Catégorie',
                'placeholder' => '-- Choisir une catégorie --',
                'class' => Category::class,
                'choice_label' => function (Category $category) {
                    return strtoupper($category->getName());
                },
                'required' => false
            ])
```
#### Dans le cas d'une relation many to many entre deux entités
Exemple un **Article** avec plusieurs **Tags**
```
            //Form/ArticleType.php

            ->add('tags',EntityType::class, [
                'class' => Tags::class,
                'multiple' => true, //on est en ManyToMany //select multiple
                'choice_label' => 'name',
                'query_builder' => function(EntityRepository $er){
                    return $er->createQueryBuilder('t')
                        ->orderBy('t.name','ASC');
                },
                 'by_reference' => false //indique qu'il ne faut pas passer par les setter mais par les 'add' (manytomany)
            ])

```

si on veut des cases à cocher
```
            //Form/ArticleType.php

            ->add('tags',EntityType::class, [
                'class' => Tags::class,
                'multiple' => true, //on est en ManyToMany
                'expanded'=> true, //case a coche
                'choice_label' => 'name',
                'query_builder' => function(EntityRepository $er){
                    return $er->createQueryBuilder('t')
                        ->orderBy('t.name','ASC');
                },
                 'by_reference' => false //indique qu'il ne faut pas passer par les setter mais par les 'add' (manytomany)
            ])

```

si on veut des bouton radio
```
            //Form/ArticleType.php

            ->add('tags',EntityType::class, [
                'class' => Tags::class,
                'multiple' => false, //on est en ManyToMany
                'expanded'=> true, 
                'choice_label' => 'name',
                'query_builder' => function(EntityRepository $er){
                    return $er->createQueryBuilder('t')
                        ->orderBy('t.name','ASC');
                },
                 'by_reference' => false //indique qu'il ne faut pas passer par les setter mais par les 'add' (manytomany)
            ])

```

### Autre possiblité, pas forcement plus pratique
selectionner plusieurs ***ecrivain** lord du formulaire de création d'un **livre**
```          //From/BookType.php
            ->add('writers', CollectionType::class, [
                'entry_type' => WriterType::class, //Form/WriterType.php doit exister
                'entry_options' => ['label' => false],
                'allow_add' => true,
            ])
```
et dans *controller article*
```
    /**
     * @Route("/biblio/add", name="add_book_biblio")
     */
    public function add(WriterRepository $writerRepository ,EntityManagerInterface $em):Response
    {
        $book = new Book();

        $writers = $writerRepository->findAll();
        
        $writer = new Writer();
        $book->addWriter($writer->setLastName('writer 1'));
        $writer2 = new Writer();
        $book->addWriter($writer2->setLastName('writer 2'));

        $form = $this->createForm(BookType::class,$book);

        //
        //ici le reste des actions

        return $this->render('biblio/add.html.twig',[
            'form' => $form->createView()
        ]);
    }
```