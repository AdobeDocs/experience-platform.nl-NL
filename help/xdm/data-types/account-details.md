---
title: Gegevenstype rekeninggegevens
description: Dit document biedt een overzicht van het gegevenstype Data Model (XDM) van het rekeningdetailervaringsgegevensmodel.
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 4%

---

# [!UICONTROL Account Details] gegevenstype

[!UICONTROL Account Details] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat details met betrekking tot een bedrijfsorganisatie beschrijft.

![Gegevenstypestructuur](../images/data-types/account-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `annualRevenue` | [[!UICONTROL Currency]](./currency.md) | Het geraamde bedrag van de jaarlijkse inkomsten van de organisatie. |
| `DUNSNumber` | Tekenreeks | Het Dun &amp; Bradstreet D-U-N-S nummer van de organisatie. Dit is een niet-indicatief getal van negen cijfers dat aan elke bedrijfslocatie in de Dun &amp; Bradstreet-database wordt toegewezen met een unieke, afzonderlijke en afzonderlijke bewerking en dat alleen door Dun &amp; Bradstreet wordt onderhouden. |
| `NAICSCode` | Tekenreeks | De indeling van de organisatie in het Noord-Amerikaanse systeem voor industriële classificatie. |
| `NAICSDescription` | Tekenreeks | Een korte beschrijving van de branche van een organisatie, die op zijn NAICS code wordt gebaseerd. |
| `SICCode` | Tekenreeks | De Standard Industrial Classification (SIC)-code van de organisatie. Dit is een code van vier cijfers die de industrie categoriseert dat de bedrijven tot op basis van hun bedrijfsactiviteiten behoren. |
| `SICDescription` | Tekenreeks | Een korte beschrijving van de branche van een organisatie, die op zijn SIC code wordt gebaseerd. |
| `companyProductAndServices` | Tekenreeks | De producten en diensten die de organisatie behandelt of zaken doet in. |
| `facebookPageUrl` | Tekenreeks | Een websitekoppeling naar de Facebook-account van de organisatie. |
| `industry` | Tekenreeks | De industrie waarvan deze organisatie deel uitmaakt. Dit is een vrije-vormgebied, en het is raadzaam om een gestructureerde waarde voor vragen te gebruiken of het `xdm:classifier` eigenschap. |
| `jigsaw` | Tekenreeks | De sleutel Data.com voor de organisatie. |
| `linkedinPageUrl` | Tekenreeks | Een websitekoppeling naar de LinkedIn-account van de organisatie. |
| `logoUrl` | Tekenreeks | Een pad dat moet worden gecombineerd met de URL van een instantie Salesforce (bijvoorbeeld `https://yourInstance.salesforce.com/`) om een URL te genereren voor het aanvragen van de afbeelding van het sociale netwerkprofiel die aan de organisatie is gekoppeld. De gegenereerde URL retourneert een HTTP-omleiding (code 302) naar de afbeelding van het sociale netwerkprofiel voor de organisatie. |
| `marketSegment` | Tekenreeks | Het marktsegment waaraan de organisatie deelneemt. Dit is een vrije-vormgebied, en het is raadzaam om een gestructureerde waarde voor vragen te gebruiken of het `xdm:identifier` eigenschap. |
| `numberOfEmployees` | Geheel | Het aantal werknemers in de organisatie. |
| `organizationType` | Tekenreeks | Een label dat het type organisatie beschrijft. |
| `primaryEmailDomain` | Tekenreeks | Het primaire e-maildomein dat de organisatie voor haar personeel gebruikt. |
| `rating` | Dubbel | De berekende score of sterwaardering voor deze organisatie. `1` de maximaal mogelijke rating aangeeft, en `0` de minimaal mogelijke rating is. |
| `tickerSymbol` | Tekenreeks | Het beurssymbool voor deze rekening. Maximaal 20 tekens. |
| `twitterHandleUrl` | Tekenreeks | Een websitekoppeling naar de twitter-handgreep van de organisatie. |
| `website` | Tekenreeks | De URL van de website van de organisatie. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.schema.json)
