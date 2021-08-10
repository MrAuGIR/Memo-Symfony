## Dans le cas ou le constructeur d'une classe representant un de nos service contient un argument particulier (float, int, string)
## qui n'est pas une dépendance qu'on peut injecter (une autre classe), il faut déclarer notre service dans le fichier services.yaml en indiquant l'argement.

**Notre service**
```
<?php

namespace App\Taxes;

use Psr\Log\LoggerInterface;

class Calculator
{
    private $float;

    public function __construct(float $tva)
    {
        $this->float = $float;
    }  
}


```

**dans le fichier services.yaml**
```
    # add more service definitions when explicit configuration is needed
    # please note that last definitions always *replace* previous ones
    App\Taxes\Calculator:
        arguments:
            $tva : 20

```