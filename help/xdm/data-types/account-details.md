---
title: Gegevenstype rekeninggegevens
description: Leer meer over het gegevenstype Data Model (XDM) van het Data Model van de Ervaring van de Rekening.
exl-id: 17254393-263e-4000-9bd2-815a9e842533
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# [!UICONTROL Account Details] gegevenstype

[!UICONTROL Account Details] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat details met betrekking tot een bedrijfsorganisatie beschrijft.

![Gegevenstypestructuur](../images/data-types/account-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `annualRevenue` | [[!UICONTROL Currency]](./currency.md) | Het geraamde bedrag van de jaarlijkse inkomsten van de organisatie. |
| `DUNSNumber` | String | Het Dun &amp; Bradstreet D-U-N-S nummer van de organisatie. Dit is een niet-indicatief getal van negen cijfers dat aan elke bedrijfslocatie in de Dun &amp; Bradstreet-database wordt toegewezen met een unieke, afzonderlijke en afzonderlijke bewerking en dat alleen door Dun &amp; Bradstreet wordt onderhouden. |
| `NAICSCode` | String | De indeling van de organisatie in het Noord-Amerikaanse systeem voor industriële classificatie. |
| `NAICSDescription` | String | Een korte beschrijving van de branche van een organisatie, die op zijn NAICS code wordt gebaseerd. |
| `SICCode` | String | De Standard Industrial Classification (SIC)-code van de organisatie. Dit is een code van vier cijfers die de industrie categoriseert dat de bedrijven tot op basis van hun bedrijfsactiviteiten behoren. |
| `SICDescription` | String | Een korte beschrijving van de branche van een organisatie, die op zijn SIC code wordt gebaseerd. |
| `companyProductAndServices` | String | De producten en diensten die de organisatie behandelt of zaken doet in. |
| `facebookPageUrl` | String | Een websitekoppeling naar de Facebook-account van de organisatie. |
| `industry` | String | De industrie waarvan deze organisatie deel uitmaakt. Dit is een vrije-vormgebied, en het is raadzaam om een gestructureerde waarde voor vragen te gebruiken of het `xdm:classifier` eigenschap. |
| `jigsaw` | String | De sleutel Data.com voor de organisatie. |
| `linkedinPageUrl` | String | Een websitekoppeling naar de LinkedIn-account van de organisatie. |
| `logoUrl` | String | Een pad dat moet worden gecombineerd met de URL van een instantie Salesforce (bijvoorbeeld `https://yourInstance.salesforce.com/`) om een URL te genereren voor het aanvragen van de afbeelding van het sociale netwerkprofiel die aan de organisatie is gekoppeld. De gegenereerde URL retourneert een HTTP-omleiding (code 302) naar de afbeelding van het sociale netwerkprofiel voor de organisatie. |
| `marketSegment` | String | Het benoemde marktpubliek waaraan de organisatie deelneemt. Dit is een vrije-vormgebied, en het is raadzaam om een gestructureerde waarde voor vragen te gebruiken of het `xdm:identifier` eigenschap. |
| `numberOfEmployees` | Geheel | Het aantal werknemers in de organisatie. |
| `organizationType` | String | Een label dat het type organisatie beschrijft. |
| `primaryEmailDomain` | String | Het primaire e-maildomein dat de organisatie voor haar personeel gebruikt. |
| `rating` | Dubbel | De berekende score of sterwaardering voor deze organisatie. `1` de maximaal mogelijke rating aangeeft, en `0` de minimaal mogelijke rating is. |
| `tickerSymbol` | String | Het beurssymbool voor deze rekening. Maximaal 20 tekens. |
| `twitterHandleUrl` | String | Een websitekoppeling naar de greep van de twitter van de organisatie. |
| `website` | String | De URL van de website van de organisatie. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.schema.json)
