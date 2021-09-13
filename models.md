# Exos Model systeem

**Lees eerst de documentatie van de gewone query builder**

Exos maakt het zeer gemakkelijk om specifieke data op te halen uit de database. Een van de tools die je kan gebruiken om met data om te gaan in je code zijn Exos Models.
Een model is een class die de `Model` class extend. De class moet genoemd worden naar de `table` dat die modeled

Een simpel voorbeeldje van een model
## voorbeeld
```php
namespace ....;

use GalactixPE\CityCore\libs\Exos\model\Model;

class Cars extends Model {


}

```


Met deze class kunnen we allerlei interessante dingen doen.

## Data ophalen uit de database
### Where selector
Je kan met de `with()` functie selecten wat je precies uit de database wilt.
```php
Cars::with("Brand", "=", "Toyota");
Cars::with("Kilometerstand", ">", 5000);
Cars::with("id", "!=", 1);
```

### Data opvragen
Om data op  te halen gebruiken we de `fetchAll(Closure $closure)` of de `firstOrNull(Closure $closure)` functies.
* `fetchAll()` returned alle matches uit de database en als er geen matches zijn dan returned de functie een lege lijst.
* `firstOrNull()` returned de eerste match en als er geen is dan returned die null.

Deze functies kun je combineren met de `with()` functie van hierboven

Alle data wordt terug meegegeven als eerste argument in de closure
```php

Cars::with("Brand", "=", "Toyota")
  ->fetchAll(function($result){
      var_dump($result);
  });
```

### Data updaten
Je kan data updaten via de `update()` functie op 2 manieren

Deze functie kun je combineren met de `with()` functie

#### 1. Via een array updaten
Met deze manier kan je meerdere columns tegelijk updaten
```php

Cars::with("Brand", "=", "Toyota")
  ->update([
      "kilometerstand" => 5000,
      "prijs" => 50000
      ]);
```

#### 2. 1 enkele column zonder array updaten
Je kan een enkele kolom ook updaten door de columnname en de value als argument mee te geven in de update functie
```php

Cars::with("Brand", "=", "Toyota")
  ->update("prijs", 50000);
```
  
  
