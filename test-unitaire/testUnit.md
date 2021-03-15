# 1 Les test unitaires
lien utile :
a https://symfony.com/doc/current/the-fast-track/fr/17-tests.html
b https://symfony.com/doc/current/testing.html#the-phpunit-testing-framework

_installer le composant suivant PHPunit pour les test unitaires_
```
symfony composer req phpunit --dev
```
###### 1 Commande symfony pour créer un class de test sur une entity 
```
symfony console make:test
```
_l'invité de commande vas ensuite vous proposer différent cas possible_
```
 Which test type would you like?:
  [TestCase       ] basic PHPUnit tests
  [KernelTestCase ] basic tests that have access to Symfony services
  [WebTestCase    ] to run browser-like scenarios, but that don't execute JavaScript code
  [ApiTestCase    ] to run API-oriented scenarios
  [PantherTestCase] to run e2e scenarios, using a real-browser or HTTP client and a real web server
```