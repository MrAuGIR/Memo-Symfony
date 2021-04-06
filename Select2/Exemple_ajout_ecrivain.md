
1. ## Dans l'entité *Book* il y a une relation ManoToMany avec *Writer*
   Dans le FormType de **Book** nous avons :
```
        $builder
            ->add('title',TextType::class,[
                'label' => 'titre du livre',
                'attr' => ['class' => 'form-control']
            ])
            ->add('description',TextareaType::class)
            ->add('publishedAt', DateType::class,[
                'label' => 'Date de publication'
            ])
            ->add('ISBN', TextType::class,[
                'label' => 'Numéro ISBN'
            ])
            ->add('types',EntityType::class, [
                'class' => Type::class,
                'multiple' => true, //on est en ManyToMany
                'expanded' => false,
                'choice_label' => 'name',
                'query_builder' => function(EntityRepository $er){
                    return $er->createQueryBuilder('t')
                        ->orderBy('t.name','ASC');
                },
                'by_reference' => false, //indique qu'il ne faut pas passer par les setter mais par les 'add' (manytomany)
                'attr' => [
                    'class' => 'select-types' //important permet de selectionner l'élément en js
                ]
            ])
            ->add('publishingHouse',EntityType::class,[
                'label' => 'Editeur',
                'placeholder' => 'choisir un Editeur',
                'class' => PublishingHouse::class,
                'choice_label' => function(PublishingHouse $publishingHouse){
                    return strtoupper($publishingHouse->getName());
                },
                'required' =>false
            ])
            ->add('writers', EntityType::class, [
                'class' => Writer::class,
                'multiple' => true,
                'expanded' => false,
                'choice_label' =>'lastName',
                'query_builder' => function(EntityRepository $er){
                    return $er->createQueryBuilder('w')
                        ->orderBy('w.lastName','ASC');
                },
                'by_reference' => false,
                'attr' => [
                    'class' => 'select-writers'
                ]
            ])
            ->add('pictures', FileType::class, [
                'label' => false,
                'multiple' => true,
                'mapped' => false,
                'required' => false
            ])
            ->add('valider', SubmitType::class)

```

2. ## Nous utilison *SELECT2* donc coté script nous avons :
```
$(function() {
        
        $('.select-writers').select2({
            tags: true,
            tokenSeparators: [',',' ']
        }).on('change', function(e){
            // on recupère les options selectionnée dans le select (this)
            let label = $(this).find("[data-select2-tag=true]"); 
            //verifie que le label selectionner n'est pas deja dans la base de donnée ou deja inserer
            if(label.length &&  $.inArray(label.val(), $(this).val() != -1)){ 
                
                fetchBiblio("/writer/add/ajax/"+label.val(),label);
                
            }
        });
    });


```
*fetchBiblio(url,element)*
```
let fetchBiblio = (url,element) =>{

    fetch(url, {
        method: "POST",
        headers: {
            "X-Requested-With": "XMLHttpRequest",
            "Content-Type": "application/json"
        }
    }).then(response => 
        response.json()
    ).then(data => {
        
        // On remplace le contenu
        //on rajoute la nouvelle option pour ne pas qu'elle ne soit encore considéré comme nouvelle
        element.innerHTML = `<option selected value="${data.id}">${element.value}</option>`;
        
    }).catch(e => alert(e));
  
}
```
3. ## Enfin coté controller nous avons
```
    /**
     * @Route("/writer/add/ajax/{label}", name="add_ajax_writer", methods={"POST"})
     */
    public function addWiterAjax(string $label,Request $request, WriterRepository $wr, EntityManagerInterface $em):Response
    {
        $writer = new Writer();

        $writer->setLastName(trim(strip_tags($label)));

        $em->persist($writer);
        $em->flush();

        $id = $writer->getId();

        return $this->json(['id' => $id],200);
    }

```