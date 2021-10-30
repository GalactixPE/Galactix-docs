# Exos Caching
Geen zin om zelf een caching systeem te maken? Dat hoeft ook helemaal niet! Als je exos models gebruikt, dan kun je gewoon het ingebouwde caching systeem gebruiken. In deze read me lees je exact hoe dat moet.

## Models voorbereiden
Voordat we beginnen is het belangrijk dat je je model "klaar maakt" om gecached te worden. Hoe doe je dit?

### Requirements
* Je table moet een:
  * Auto_increment column hebben, die ook een primary key is
  * Een gewone primary key die niet zijn value krijgt op de MySQL server.
* Model registreren
* Model moet de Cacheable interface implementen

### De models registreren
Het is de bedoeling dat je elke model die je gebruikt, registreert bij de Exos ModelManager.
```php
public function onEnable(): void
{
  ModelManager::register(TestModel::class);
}
```

### Cacheable interface implementen
Elke model class die gecached moet worden, moet de `Cacheable` interface implementeren
```php
class TestModel extends Model Implements Cacheable {

  

}
```

### Primary key column
Als de primary key column **niet** `id` heet, dan moet je dit aangeven in de Model class. Dit doe je door de `protected $primaryKeyColumn` property te herdefinieren. 
```php
class TestModel extends Model Implements Cacheable {

  protected $primaryKeyColumn = "id";

}
```


Voila klaar is kees! Nu ben je helemaal klaar om de caching features van Exos te gebruiken.

De data wordt opgeslagen naar de database:
* Wanneer de server uitgaat
* Om de x ticks
* Als er expliciet wordt gevraagd om de cache op te slaan met `CacheManager::saveCache()`
