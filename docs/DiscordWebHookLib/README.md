# Discord Webhook Library

### Maak webhook instantie
Om een webhook te maken zul je een webhook URL moeten hebben.
```php
$webHook = new DiscordWebHook("WEBHOOK URL");
```
---

### Maken van message
Om een message te maken zul je een `WebHookMessage` moeten gaan maken.
In die message kun je verschillende dingen aanpassen.
* `Content` (Gewoon het bericht met een limiet van 2000 characters)
* `Username` (Username die word gebruikt bij het bericht)
* `AvatarUrl` (URL van profiel foto)
* `TextToSpeech` (Of het bericht een text to speech bericht is.)
* `Embed` (Embeds voor het bericht)

Voorbeeld:
```php
$webHook = new DiscordWebHook("Webhook URL");

$msg = new WebHookMessage();
$msg->setUsername("USERNAME")
    ->setAvatarURL("https://galactixpe.nl/epicimage.png");
    ->setContent("Epic bericht!");

$webHook->send($msg);
```
---
### Embeds
Ook kun je dus embeds maken via deze library.
Embed hebben 2 must have opties:

* `Title` (Titel van de embed)
* `Description` (Stuk tekst dat onder de titel staat)

Daarnaast zijn er nog 7 extra functies:

* `Author` (Author van de embed met profile URL)
* `Color` (De kleur die de embed heeft, hiervoor kun je ook `EmbedColor` gebruiken, deze kleuren zijn gebasseerd op Bootstrap)
* `Fields` (Verschillende substukjes die je kunt hebben in een embed.)
* `Thumbnail` (Kleinere afbeelding in de embed)
* `Image` (Grote afbeelding in embed)
* `Footer` (Tekst die in de footer komt te staan)
* `Timestamp` (Timestamp van de embed)

Voorbeeld:
```php

$webHook = new DiscordWebHook("Webhook URL");

$msg = new WebHookMessage();

$embed = Embed::create("Titel", "Beschrijving")
         ->setColor(EmbedColor::SUCCESS)
         ->setFooter("Epische footer tekst");

$msg->addEmbed($embed);

$webHook->send($msg);

```

