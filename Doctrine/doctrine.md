# Communiquer avec la base de donnée via doctrine dans symfony


## 1 - avec les méthodes implémenté dans le controlleur par la class **abstractControlleur**

###### sans utiliser l'injection de dépendance appeler le repository de la class souhaité pour ensuite récupérer un ou plusieurs élément dans la bdd
```
    /**
     * @Route("/product/{id}", name="product_show")
     */
    public function show(int $id): Response
    {
        // On va chercher le product correspondant
        $manager = $this->getDoctrine()->getManager();

        $product = $manager->getRepository(Product::class)->find($id);

```

###### ou directement de la façon suivante
```
     /**
     * @Route("/product/{id}", name="product_show")
     */
    public function show(int $id): Response
    {
        $product = $this->getDoctrine()
                        ->getRepository(Product::class)
                        ->find($id);


```

###### ou en utilisant l'injection de dépendance pour recupéré ProductRepository
```
    /**
     * @Route("/product/{id}", name="product_show")
     */
    public function show(int $id, ProductRepository $productRepository): Response
    {
        $product = $productRepository->find($id);


```

###### ou encore directement en injectétant l'object avec l'id présent en paramètre dans la route
```
    /**
     * @Route("/product/{id}", name="product_show")
     */
    public function show(Product $product): Response
    {
        

```

## 2 - Methode disponible avec un objet de class repository
```
    $repository = $this->getDoctrine()->getRepository(Product::class);

    // recupérer un produit en fonction de son id
    $product = $repository->find($id);

    // recupérer un produit en fonction du critére 'name'
    $product = $repository->findOneBy(['name' => 'Keyboard']);

    // ou en ajoutant un autre critère
    $product = $repository->findOneBy([
        'name' => 'Keyboard',
        'price' => 1999,
    ]);

    // si on veut récupérer plusieurs produit en fonction de critères
    $products = $repository->findBy(
        ['name' => 'Keyboard'],
        ['price' => 'ASC']
    );

    // recupérer tous les produits de la base de donnée
    $products = $repository->findAll();


```

## 3 Crée un nouvel objet en allant chercher l'objet entityManager via _$this->getDoctrine()_
```
    /**
     * @Route("/product", name="create_product")
     */
    public function createProduct(): Response
    {
        // you can fetch the EntityManager via $this->getDoctrine()
        // or you can add an argument to the action: createProduct(EntityManagerInterface $entityManager)
        $entityManager = $this->getDoctrine()->getManager();

        $product = new Product();
        $product->setName('Keyboard');
        $product->setPrice(1999);
        $product->setDescription('Ergonomic and stylish!');

        // tell Doctrine you want to (eventually) save the Product (no queries yet)
        $entityManager->persist($product);

        // actually executes the queries (i.e. the INSERT query)
        $entityManager->flush();

```

###### ou en utilisant EntityManagerInterface $em en paramètre de la méthode
```
    /**
     * @Route("/product", name="create_product")
     */
    public function createProduct(EntityManagerInterface $em): Response
    {
    
        $product = new Product();
        $product->setName('Keyboard');
        $product->setPrice(1999);
        $product->setDescription('Ergonomic and stylish!');

        // sauvegarde le produit en attente de la requète create
        $em->persist($product);

        // execution de la requète
        $emr->flush();

```

## 4 mettre un jour un produit

```
    /**
     * @Route("/product/edit/{id}")
     */
    public function update(int $id): Response
    {
        $entityManager = $this->getDoctrine()->getManager();
        $product = $entityManager->getRepository(Product::class)->find($id);

        if (!$product) {
            throw $this->createNotFoundException(
                'No product found for id '.$id
            );

            //ou

            $this->addflash('warning','produit non trouvé');
            return $this->redirectToRoute('home');
        }

        $product->setName('nouveau nom');
        $entityManager->flush();

        return $this->redirectToRoute('product_show', [
            'id' => $product->getId()
        ]);
    }

```
_en utilisant l'injection de dépendance nous avons une autre façon d'écrire cette methode_
```
    /**
     * @Route("/product/edit/{id}")
     */
    public function update(Product $product, EntityManagerInterface $em): Response
    {
        
        if (!$product) {
           
            $this->addflash('warning','produit non trouvé');
            return $this->redirectToRoute('home');
        }

        $product->setName('nouveau nom');
        $em->flush();

        return $this->redirectToRoute('product_show', [
            'id' => $product->getId()
        ]);
    }

```
