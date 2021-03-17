```
<?php
namespace App\DataFixtures;

use App\Entity\Biblio;
use App\Entity\User;
use Faker\Factory;
use Doctrine\Persistence\ObjectManager;
use Bluemmb\Faker\PicsumPhotosProvider;
use Doctrine\Bundle\FixturesBundle\Fixture;
use Symfony\Component\String\Slugger\SluggerInterface;
use Symfony\Component\Security\Core\Encoder\UserPasswordEncoderInterface;

class AppFixtures extends Fixture
{
    protected $slugger;
    protected $passwordEncoder;


    public function __construct(SluggerInterface $slugger, UserPasswordEncoderInterface $passwordEncoder)
    {
        $this->slugger = $slugger;
        $this->passwordEncoder = $passwordEncoder;
    }
    public function load(ObjectManager $manager)
    {
        $faker = Factory::create('fr_FR');
        $faker->addProvider(new PicsumPhotosProvider($faker));

        

        /* Utilisateurs */
        $admin = new User();
        $admin->setEmail('augirard17@gmail.com');
        $admin->setPassword($this->passwordEncoder->encodePassword($admin, 'password'));
        $admin->setRegisterAt(new \DateTime('now'))
              ->setRoles(['ROLE_ADMIN'])
        ;
        $manager->persist($admin);

        /*Biblio admin */
        $biblo = new Biblio();
        $biblo->setCreatedAt(new \DateTime('now'))
              ->setTitle('Admin Biblio')
              ->setSlug(strtolower($this->slugger->slug($biblo->getTitle())))
              ->setUserOwner($admin)
        ;
        $manager->persist($biblo);


        
        $manager->flush();
    }
}


```