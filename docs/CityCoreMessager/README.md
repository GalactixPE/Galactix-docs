# CityCore Messager

Voor al onze messages maken we gebruik van CityCoreMessager

In ons systeem kennen we 5 soorten messages:
- Info messages
- Error messages
- Success messages
- Warning messages
- List messages

Deze messages worden op deze manier gebruikt zodat we snel message formats kunnen aanpassen.
<hr>

### Message formating
Ook hebben we bepaalde message formatting die je kunt gebruiken om bepaalde strings duidelijker aan te kunnen geven.
Dit kun je daarvoor gebruiken.

**Highlighting**
> **%HL%** Message **%HL_END%**

**Bold text**
> **%B%** Message **%B_END%**

<hr>

### Info Message
```php
CityCoreMessager::info($receiver, $moduleName, $message);

// Bijvoorbeeld:
CityCoreMessager::info($player, "Plots", "Dit plot is van: %HL%" . $plotOwnerName . "%HL_END%");
```

### Error Message
```php
CityCoreMessager::error($receiver, $moduleName, $message);

// Bijvoorbeeld:
CityCoreMessager::error($sender, "UniPerms", "Groep %HL%".$groupName."%HL_END% bestaat al.");
```

### Success Message
```php
CityCoreMessager::success($receiver, $moduleName, $message);

// Bijvoorbeeld:
CityCoreMessager::success($sender, "UniPerms", "Groep %HL%".$groupName."%HL_END% bestaat al.");
```

### Warning Message
```php
CityCoreMessager::warning($receiver, $moduleName, $message);

// Bijvoorbeeld:
CityCoreMessager::warning($this->player, "GPS", "Je bent te ver afgeweken van de berekende route, een nieuwe route wordt gezocht");
```

### List Message
List messages zijn een klein stukje uitgebreider en hebben wat extra data nodig.

```php
CityCoreMessage::list($receiver, $listTitle, $itemsPerPage, $pageNumber, $arrayList, $numeric)

CityCoreMessager::list($sender, "UniPerms Groups", 5, $page, $groupNames, false);
```
