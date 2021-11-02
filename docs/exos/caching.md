# Caching

Geen zin om zelf een caching systeem te maken? Dat hoeft ook helemaal niet! Als je exos models gebruikt, dan kun je gewoon het ingebouwde caching systeem gebruiken. In deze read me lees je exact hoe dat moet.

## Models voorbereiden

Voordat we beginnen is het belangrijk dat je je model "klaar maakt" om gecached te worden. Hoe doe je dit?

### Requirements

- Je table moet een:
  - Auto_increment column hebben, die ook een primary key is
  - Een gewone primary key die niet zijn value krijgt op de MySQL server.
- Model registreren
- Model moet de Cacheable interface implementen

### De models registreren

Het is de bedoeling dat je elke model die je gebruikt, registreert bij de Exos ModelManager.

```php
<?php

public function onEnable(): void
{
  ModelManager::register(TestModel::class);
}
```

### Cacheable interface implementen

Elke model class die gecached moet worden, moet de `Cacheable` interface implementeren

```php
<?php

class TestModel extends Model Implements Cacheable {



}
```

### Primary key column

Als de primary key column **niet** `id` heet, dan moet je dit aangeven in de Model class. Dit doe je door de `protected $primaryKeyColumn` property te herdefinieren.

```php
<?php

class TestModel extends Model Implements Cacheable {

  protected $primaryKeyColumn = "id";

}
```

Voila klaar is kees! Nu ben je helemaal klaar om de caching features van Exos te gebruiken. Wanneer de server opstart zal alle data in memory worden opgenomen.

De data wordt opgeslagen naar de database:

- Wanneer de server uitgaat
- Om de x ticks
- Als er expliciet wordt gevraagd om de cache op te slaan met `CacheManager::saveCache()`

## Selector
Soms kan het zijn dat je slechts een specifiek deel van de data wilt. In dat geval kun je gebruik maken van de selectors in Exos. Deze selectors worden uitgebreid besproken in de **model docs.** 

Kort samengevat, je kan de `where()` functie gebruiken om te specifieren aan welke voorwaarde de data waarop je de query zal uitvoeren moet voldoen.

```php
<?php

Car::cache()->where("brand", "=", "toyota");

```

## Gecachte data ophalen
### Inleiding
Je kan zoals bij gewone models, data ophalen. Bij gecachte models gaat dit een heeeeeeeeeel klein beetje anders, echt waar. Het enige wat je moet doen is `cache()` toevoegen na de modelnaam en voila! Je kan al je favoriete functies gebruiken om je data op te halen.

```php linenums="1"
<?php

Car::cache()->fetchAll();

```

### Data fetchen
Nadat je hebt gespecifieerd aan welke voorwaarde de data moet voldoen, kun je kiezen om **alle data** of slechts **een rij** uit de cache op te halen.

Je kan ook makkelijk data ophalen adhv de primary key met de `get()` functie. De get functie zal snel de data ophalen met de gevraagde primary key. Aangezien primary keys `unique` zijn, zal je slechts één resultaat krijgen.

!!! info
  De primary key wordt gedefinieerd in de model class. Zie //wip link inserten.

```php
<?php

// haalt alle data op
Car::cache()->where("brand", "=", "toyota")->fetchAll();

// haalt slechts 1 rij op uit de cache
Car::cache()->where("brand", "=", "toyota")->firstOrNull();

// haalt de data op adhv de primary key
Car::cache()->get(10);

```
!!! warning
  De fetchAll() en firstOrNull() functie returnen allebei direct de data. Dus het is niet nodig om een closure mee te geven. Mocht je closures leuker vinden, dan kun je die ook gebruiken.

## Gecachte data updaten





