# Les voters

Permet de déterminer si l'utilisateur connecté à la permission pour réaliser certaines actions sur un objet

**lien utile** : https://symfony.com/doc/current/security/voters.html


1. ###### Exmple de fichier
    ```
    <?php
    namespace App\Security\Voter;

    use App\Entity\User;
    use App\Entity\Transport;
    use Symfony\Component\Security\Core\Security;
    use Symfony\Component\Security\Core\Authentication\Token\TokenInterface;
    use Symfony\Component\Security\Core\Authorization\Voter\Voter;

    class TransportVoter extends Voter
    {
        const VIEW = "view";
        const EDIT = "edit";
        const CREATE = 'create';
        const DELETE = 'delete';
        const MANAGE = 'manage';

        private $security;

        public function __construct(Security $security)
        {
            $this->security = $security;
        }

        protected function supports(string $attributes, $subject)
        {

            //Si l'attribut fait partie de ceux supportés et 
            //on vote seulement avec un objet de class Transport
            return \in_array($attributes,[self::VIEW, self::EDIT, self::CREATE, self::DELETE, self::MANAGE]) && ($subject instanceof Transport);

        }

        protected function voteOnAttribute(string $attribute, $subject, TokenInterface $token)
        {
            $user = $token->getUser();

            if(!$user instanceof User){
                //si l'utilisateur n'est pas logger, deny access
                return false;
            }

            //Si je suis l'administrateur j'ai tous les droit
            if($this->security->isGranted('ROLE_ADMIN')){
                return true;
            }

            //si on est là, c'est que $subject est un objet transport
            /** @var Transport $transport */
            $transport = $subject;

            switch($attribute){
                case self::VIEW:
                    return true;
                case self::CREATE:
                    return true;
                case self::EDIT:
                    return $transport->getUser() == $user;
                case self::DELETE:
                    return $transport->getUser() == $user;
                case self::MANAGE:
                    return $transport->getUser() == $user;
            }

            return false;
        }


    }

    ```
2. ### PLacer le fichier dans /src/security/Voter


3. ### utilisation du voter créé
   ```
     /*on verifie que l'utilisateur connecté est le 'proprietaire' du ticket*/
    if(!$this->isGranted('delete',$ticket)){
        $this->addFlash('danger','action non autorisé');
        return $this->redirectToRoute('transport_show',['transport_id'=> $transport_id]);
    }
   ```










