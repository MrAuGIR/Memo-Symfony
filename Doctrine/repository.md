#1 Personnaliser les requètes avec la base de données dans la class Repository 



#### a - __createQuery()__
```
class ProductRepository extends ServiceEntityRepository
{
    public function __construct(ManagerRegistry $registry)
    {
        parent::__construct($registry, Product::class);
    }

    /**
     * @return Product[]
     */
    public function findAllGreaterThanPrice(int $price): array
    {
        $entityManager = $this->getEntityManager();

        $query = $entityManager->createQuery(
            'SELECT p
            FROM App\Entity\Product p
            WHERE p.price > :price
            ORDER BY p.price ASC'
        )->setParameter('price', $price);

        // retourne un tableau d'object Product
        return $query->getResult();
    }
}

```

#### b - __queryBuilder()__
```
class ProductRepository extends ServiceEntityRepository
{
    public function findAllGreaterThanPrice(int $price, bool $includeUnavailableProducts = false): array
    {
        // Product est automatiquement selectionné
        // the "p" est un allias utilisé dans le reste de la requète
        $qb = $this->createQueryBuilder('p')
            ->where('p.price > :price')
            ->setParameter('price', $price)
            ->orderBy('p.price', 'ASC');

        if (!$includeUnavailableProducts) {
            $qb->andWhere('p.available = TRUE');
        }

        $query = $qb->getQuery();

        return $query->execute();

        // to get just one result:
        // $product = $query->setMaxResults(1)->getOneOrNullResult();
    }
}

```

#### c - en ecrivant directement la requète
```
class ProductRepository extends ServiceEntityRepository
{
    public function findAllGreaterThanPrice(int $price): array
    {
        $conn = $this->getEntityManager()->getConnection();

        $sql = '
            SELECT * FROM product p
            WHERE p.price > :price
            ORDER BY p.price ASC
            ';
        $stmt = $conn->prepare($sql);
        $stmt->execute(['price' => $price]);

        // returns an array of arrays (i.e. a raw data set)
        return $stmt->fetchAllAssociative();
    }
}
```

### d - exemple de requètes
```
    /**
     * Returns Annonces between 2 dates
     */
    public function selectInterval($from, $to, $cat = null){

        $query = $this->createQueryBuilder('a')
            ->where('a.created_at > :from')
            ->andWhere('a.created_at < :to')
            ->setParameter(':from', $from)
            ->setParameter(':to', $to);
        if($cat != null){
            $query->leftJoin('a.categories', 'c')
                ->andWhere('c.id = :cat')
                ->setParameter(':cat', $cat);
        }
        return $query->getQuery()->getResult();
    }

    /**
     * retourne les produits par page (pagination)
     * @return void
     * @param $page page en cours
     * @param $limit nombre de produit par page 
     */
    public function getPaginatedAnnonces($page, $limit, $filters = null){
        $query = $this->createQueryBuilder('p')
            ->where('p.active = 1');

        // On filtre les produits par catégorie
        if($filters != null){
            $query->andWhere('p.categories IN(:cats)')
                ->setParameter(':cats', array_values($filters)); //filters est un tableau key=>value de critère
        }

        $query->orderBy('p.created_at')
            ->setFirstResult(($page * $limit) - $limit)
            ->setMaxResults($limit)
        ;
        return $query->getQuery()->getResult();
    }

    /**
     * Retourn le nombre de produit
     * @return void 
     */
    public function getTotalProduct($filters = null){
        $query = $this->createQueryBuilder('p')
            ->select('COUNT(p)')
            ->where('p.active = 1');
        // On filtre les produits par catégorie
        if($filters != null){
            $query->andWhere('p.categories IN(:cats)')
                ->setParameter(':cats', array_values($filters));
        }

        return $query->getQuery()->getSingleScalarResult();
    }


```