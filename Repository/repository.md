# Les requètes avec la base de donnée dans symfony

## 

```

    // On va chercher le commentaire correspondant
    $manager = $this->getDoctrine()->getManager();

    $comment = $manager->getRepository(Comments::class)->find($id);

```

