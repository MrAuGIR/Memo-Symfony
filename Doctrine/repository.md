# Communiquer avec la base de donnée via doctrine dans symfony

## 
 1 - avec les méthodes implémenté dans le controlleur par la class **abstractControlleur**

```

    // On va chercher le commentaire correspondant
    $manager = $this->getDoctrine()->getManager();

    $product = $manager->getRepository(Product::class)->find($id);

```

#### ou sans passer par une variable manager

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
### ou en utilisant l'injection de dépendance pour recupéré ProductRepository

```
    /**
     * @Route("/product/{id}", name="product_show")
     */
    public function show(int $id, ProductRepository $productRepository): Response
    {
        $product = $productRepository->find($id);


```

### ou encore directement en injectétant l'object avec l'id présent en paramètre dans la route

```
    /**
     * @Route("/product/{id}", name="product_show")
     */
    public function show(Product $product): Response
    {
        


```