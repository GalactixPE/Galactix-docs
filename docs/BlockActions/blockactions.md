# BlockActions
BlockActions is een handige API om snel blocks te linken aan bepaalde acties. Merk op dat ik het woord "acties" en niet "commands" gebruik. Dat is omdat je ook bepaalde functies kan laten runnen wanneer er wordt geinteract met een ActionBlock.

## Types
Er zijn twee verschillende ActionBlocks:
* Handler: deze triggeren interne code
* Command: triggeren een lijst van commands die wordt ingesteld.

## Command ActionBlock
Dit type ActionBlock is eigenlijk heel straight-forward. Je maakt **in-game** een ActionBlock aan met de command `/actionblock create <name> <type> <command>`. 

* `name`: de naam van de actionblock (moet uniek zijn per ActionBlock)
* `type`: in dit geval gewoon `command`
* `command`: een Minecraft command zonder `/`

Daarna moet je de block waarvan je een ActionBlock wilt maken breken. Tada! De ActionBlock is aangemaakt.

## Handler ActionBlock
Dit type ActionBlock is veel interessanter. We kunnen met dit type heel makkelijk functies aanroepen in onze code zonder te veel extra code bij te maken. Wat je eerst moet doen is simpelweg in jouw code een handler registreren bij de ActionBlock plugin.

Dit doe je als volgt:

```php
<?php

BlockActionModule::registerHandler("een_naam", function(PlayerInteractEvent $event){
  // zet hier code die runt wanneer wordt geintereact met de block.
});
```

De closure die je meegeeft wordt aangeroepen wanneer wordt geinteract met een ActionBlock met de naam `een_naam`. Dus wat je nu nog moet doen is in-game een ActionBlock aanmaken met de volgende command:

`/actionblock create <name> <type> <command>`. 

* `name`: de naam van de actionblock (moet **niet** uniek zijn per ActionBlock, je kan meerdere ActionBlocks dezelfde naam geven. Geldt alleen voor Handler ActionBlocks)
* `type`: `handler`

Daarna moet je de block waarvan je een ActionBlock wilt maken breken. Voila! Je code in de closure zal nu uitvoeren wanneer een speler interact met de block.

## Coole feautures
* Cooldown van 1 seconde op elke interaction
* Idk, het is makkelijk om mee te werken?

