#
#### Commande authentification
`` php bin/console make:auth ``

#### Chemin du logout à définir
dans la fonction  onAuthenticationSuccess de la class Authenticator
exemple : ``  return new RedirectResponse($this->urlGenerator->generate('article_home')); ``

