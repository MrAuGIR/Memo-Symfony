
###### Pour eviter la reference circulaire lors de la normalization d'objet
on peut dans les entité indiquer quels champs peuvent être normalizer, avec des annotations
``use Symfony\Component\Serializer\Annotation\Groups;``

```
    /**
     * @ORM\Id
     * @ORM\GeneratedValue
     * @ORM\Column(type="integer")
     * @Groups("post:read")
     */
    private $id;
```
toute donnée/champs qui ne sera pas *tagué* par @Groups ne sera pas pris en compte

mais pour cela il faut aussi indiquer à la méthode normalize une option

``$postsNormalises = $normalizerInterface->normalize($posts,null,['groups' => 'post:read']);``

avec la méthode serialize

```
    /**
     * @Route("/api/post", name="api_post")
     */
    public function index(PostRepository $postRepository, SerializerInterface $serializerInterface): Response
    {
        $posts = $postRepository->findAll();

        // $postsNormalises = $normalizerInterface->normalize($posts,null,['groups' => 'post:read']);

        // $json = json_encode($postsNormalises);

        $json = $serializerInterface->serialize($posts, 'json', ['groups' => 'post:read']);

        $response = new Response($json, 200, [
            "content-type" => "application/json"
        ]);

        return $response;
    }
```

##### en remplaçant ___new response__ par __new JsonResponse__

``$response = new JsonResponse($json,200,[],true);``


##### en simplifiant encore
```
    /**
     * @Route("/api/post", name="api_post")
     */
    public function index(PostRepository $postRepository, SerializerInterface $serializerInterface): Response
    {
        $posts = $postRepository->findAll();

        
        $response = $this->json($posts, 200, [], ['groups'=>'post:read']);

        return $response;
    }
```

enfin

```
/**
     * @Route("/api/post", name="api_post")
     */
    public function index(PostRepository $postRepository, SerializerInterface $serializerInterface): Response
    {

        return $this->json($postRepository->findAll(), 200, [], ['groups'=>'post:read']);
    }
}
```