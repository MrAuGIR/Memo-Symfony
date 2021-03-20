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
