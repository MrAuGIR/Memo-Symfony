# 1 installer CKEditor

### A installation du bundle
```
composer require friendsofsymfony/ckeditor-bundle
```

### B installation du de ckeditor dans le projet
```
php bin/console ckeditor:install
```

### C installation des assets dans le dossier public
```
php bin/console assets:install public
```

### D Utiliser CKeditor dans un formType d'une entité
ajouter le use :
`` use FOS\CKEditorBundle\Form\Type\CKEditorType; ``
puis modifier les TextareaType
```
        ->add('description', CKEditorType::class, [
            'label' => "Description de l'évênement",
            'attr' => [
                'placeholder' => "Une description de l'évênement"
            ],
            'required' => false
        ])
```