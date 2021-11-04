# Economy

Hoe werkt Plot selling nu precies?

!!! info

     Deze documentatie is vooral voor mezelf gemaakt (Mohamed), zodat ik beter begrijp hoe mijn eigen systeem werkt :). Er spelen veel factoren een rol in het bepalen of een plot mag verkocht worden of niet.

## Plot kopen van de gemeente
Stel dat je een plot wilt kopen van de gemeente. Welke factoren spelen dan een rol in het bepalen of je dat plot wel kan kopen of niet.

* `defaultSellPrice` bepaalt de prijs
* Als `defaultSellPrice` wordt ingesteld naar `-1` dan kan het plot niet gekocht worden van de gemeente.
* Als het plot al een eigenaar heeft dan kan het niet gekocht worden.

## Plot (ver)kopen van/aan een speler
* Als `isSellable` wordt ingesteld naar `false`, dan kan het plot niet verkocht worden.
* `sellPrice` bepaalt de verkoopprijs van het plot
* Als `sellPrice` niet gelijk is aan `null`, dan betekent dat dat het plot verkocht wordt en kan gekocht worden door een speler.

!!! danger

    mohamed is een noob, maar datalion ook.
    `noobheid(Mohamed) > noobheid(DataLion)`