---
title: Gebruikersmachtigingen voor tags
description: Leer over de verschillende soorten toestemmingen beschikbaar voor markeringen en sommige basisimplementatiestrategieën voor verschillende zaken van bedrijfsgebruik.
exl-id: 9b48847a-6133-4dbd-b17d-e7b88152ad7d
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1308'
ht-degree: 1%

---

# Gebruikersmachtigingen voor tags

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Gebruikersmachtigingen voor tags in Adobe Experience Platform worden aan gebruikers toegewezen via Adobe Admin Console. In plaats van te worden toegewezen aan individuele gebruikers, worden verschillende reeksen toestemmingen gevormd afzonderlijk als productprofielen. De gebruikers worden dan toegewezen aan deze productprofielen om de toestemmingen te worden verleend zij voor zijn gevormd.

Deze gids verstrekt een overzicht van de verschillende soorten toestemmingen beschikbaar voor markeringen, de functionaliteit zij toegang tot, en sommige basisimplementatiestrategieën voor verschillende zaken van bedrijfs gebruik verlenen.

>[!NOTE]
>
>Voor stappen over hoe te om toestemmingen voor gebruikers te vormen die Admin Console gebruiken, gelieve te verwijzen naar het leerprogramma op [machtigingen voor gegevensverzameling beheren](../../../collection/permissions.md).

## Machtigingstypen

Binnen een productprofiel worden de machtigingen voor tags onderverdeeld in vier categorieën:

1. Platforms
1. Properties
1. Eigendomsrechten
1. Bedrijfsrechten

### Platforms

Elke eigenschap tag heeft een platform. Er zijn momenteel twee platforms die u voor tags kunt gebruiken: Web en mobiel. U kunt dit toestemmingstype gebruiken om toegang tot een bepaald type van bezit te beperken of te verlenen. Dit kan handig zijn als het team dat uw mobiele apps beheert, anders is dan het team dat uw websites beheert.

### Eigenschappen

Standaard bieden productprofielen toegang tot alle eigenschappen die binnen uw bedrijf bestaan, zowel momenteel als in de toekomst. Gebruikend dit toestemmingstype, kunt u toegang tot specifieke bestaande eigenschappen door naam beperken of verlenen.

### Eigendomsrechten {#property-rights}

Om het even welk markeringsbezit dat u in UI creeert wordt beschikbaar in Admin Console, die u toestaat om het bezit met specifieke bezitsrechten in het zelfde productprofiel te groeperen.

Als een bepaald productprofiel bijvoorbeeld geen toegang heeft tot Eigenschap A1, kunnen gebruikers die tot dat profiel behoren geen instellingen zien of wijzigen binnen Eigenschap A1.

Als een gebruiker tot een profiel behoort dat toegang tot Bezit A1 heeft, worden de acties zij binnen Bezit A1 kunnen uitvoeren bepaald door de rechten zij van dit profiel zijn verleend. Als een gebruiker toestemmingen voor Bezit A1 maar geen toegewezen rechten heeft, dan hebben zij read-only toegang voor dat bezit.

De volgende tabel geeft een overzicht van de beschikbare eigendomsrechten en de functies die zij toegang verlenen tot:

| Eigenschappenrecht | Beschrijving |
| --- | --- |
| **Ontwikkelen** | Op deze manier kunt u de volgende handelingen uitvoeren:<ul><li>Regels en gegevenselementen maken</li><li>Bibliotheken maken en deze bouwen in bestaande ontwikkelomgevingen</li><li>Bibliotheek ter goedkeuring verzenden</li></ul>De meeste dagelijkse taken in UI vereisen dit recht. |
| **Goedkeuren** | Hierdoor kunt u een verzonden bibliotheek gebruiken en bouwen naar de testomgeving. U kunt ook een bibliotheek goedkeuren voor publicatie nadat het testen is voltooid. |
| **Publicatie** | Hierdoor kunt u goedgekeurde bibliotheken publiceren naar de productieomgeving. |
| **Extensies beheren** | Op deze manier kunt u de volgende handelingen uitvoeren: <ul><li>Nieuwe extensies installeren op een eigenschap</li><li>De configuratie voor een reeds geïnstalleerde extensie wijzigen</li><li>Een extensie verwijderen</li></ul>Raadpleeg de documentatie bij het overzicht van extensies voor [meer informatie over extensies](../managing-resources/extensions/overview.md). Deze rol behoort gewoonlijk tot IT of Marketing, afhankelijk van uw organisatie. |
| **Omgevingen beheren** | Hierdoor kunt u omgevingen maken en wijzigen. Zie de [omgevingdocumentatie](../publishing/environments.md) voor meer informatie . Deze rol behoort gewoonlijk tot de IT-groep. |

{style=&quot;table-layout:auto&quot;}

### Vennootschapsrechten

De rechten van het bedrijf zijn op toestemmingen van toepassing die veelvoudige eigenschappen overspannen.  Deze worden in de onderstaande tabel beschreven:

| Bedrijfsrecht | Beschrijving |
| --- | --- |
| **Eigenschappen beheren** | Op deze manier kunt u de volgende handelingen uitvoeren:<ul><li>Nieuwe eigenschappen maken</li><li>Metagegevens en instellingen op eigenschapsniveau wijzigen</li><li>Eigenschappen verwijderen</li></ul>Beheerders voeren deze rol gewoonlijk uit. Zie de [eigenschappendocumentatie](companies-and-properties.md) voor meer informatie . |
| **Extensies ontwikkelen** | Biedt de mogelijkheid extensiepakketten te maken en aan te passen die eigendom zijn van het bedrijf, inclusief privéreleases en verzoeken om openbare publicatie. |
| **App Configurations beheren** | Dit is alleen beschikbaar als u een licentie voor Adobe Journey Optimizer hebt of een andere oplossing die toegang biedt tot mobiele berichten in de app en push-berichten.  Op deze manier kunt u de apps beheren die Experience Cloud bekend zijn, samen met de vereiste pushreferenties om te communiceren met de Firebase Cloud Messaging-service en de Apple Push Notification Service. |

{style=&quot;table-layout:auto&quot;}

## Totaal aantal gebruikersmachtigingen

Het totale aantal machtigingen van een individuele gebruiker wordt bepaald door het totale aantal gebruikers in verschillende productprofielen. Als een gebruiker tot meerdere productprofielen behoort, worden de machtigingen van elk profiel bij elkaar opgeteld in plaats van vermenigvuldigd.

Met Productprofiel A hebt u bijvoorbeeld het ontwikkelrecht voor Eigenschap 1. Met Productprofiel B hebt u het recht Publiceren voor Eigenschap 2. In dit geval kunt u Ontwikkelen in Eigenschap 1 en Publiceren in Eigenschap 2, maar u kunt niet publiceren in Eigenschap 1 of Ontwikkelen in Eigenschap 2 omdat hiervoor geen expliciete rechten zijn verleend.

## Rechtenscenario&#39;s

Verschillende bedrijven hebben verschillende behoeften bij het maken van nieuwe productprofielen. Deze behoeften variëren afhankelijk van bedrijfsgrootte, organisatiestructuur, het aantal plaatsen, het aantal mensen betrokken bij het beheren van markeringen, etc.

Hieronder vindt u een aantal algemene scenario&#39;s en een aanbevolen beginpunt voor het maken van productprofielen en het toevoegen van gebruikers aan deze profielen.

### Eenpersoonshow

Als u een klein bedrijf in werking stelt dat één persoon met alles heeft, geef deze gebruikerstoestemmingen voor alle eigenschappen toe en wijs hen alle hierboven vermelde rechten toe.

### Scheiding van taken

Overweeg een situatie waarin veel mensen in uw organisatie betrokken zijn bij het labelen. U hebt één groep personen (zoals een externe consultant) die regels en gegevenselementen maakt, maar u wilt niet dat zij toegang hebben tot de productieomgeving. In dit geval, wilt u ervoor zorgen dat niemand aan Productie behalve het team van IT opstelt.

U doet dit als volgt:

1. Maak een account voor uw consultants en geef deze alleen het recht Ontwikkelen.
1. De consultant bouwt en test binnen de grenzen die u instelt.
1. Als de consultant een nieuwe extensie wil of klaar is om live te gaan, voert een vertegenwoordiger van uw organisatie (met de juiste rechten) deze acties uit.

### Enterprise

Een ondernemingsbedrijf zou veelvoudige plaatsen kunnen hebben die geografisch, met verschillende teams verantwoordelijk voor elke geo worden verdeeld. Binnen die teams ontwikkelen en publiceren verschillende personen zich.

Dit is vergelijkbaar met &quot;Scheiding van rechten&quot; hierboven, maar georganiseerd per geografisch gebied. U kunt bijvoorbeeld een ontwikkelprofiel en een publicatieprofiel voor Noord-Amerika maken en aparte groepen voor Ontwikkelen en Publiceren voor Europa maken.

## Voorbeeldrollen

De volgende lijst verstrekt sommige voorbeelden van de soorten rollen u in uw organisatie zou kunnen hebben en welke toestemmingen u hen zou moeten toewijzen:

| Rol | Beschrijving | Eigenschappen | Eigendomsrechten | Bedrijfsrechten |
| --- | --- | --- | --- | --- |
| Manager | Wil zien wat er in het systeem gebeurt, maar mag geen wijzigingen kunnen aanbrengen. | Automatisch opnemen | (Geen) | (Geen) |
| De markt | Kan extensies installeren en nieuwe tags instellen voor bestaande eigenschappen, maar kan niet publiceren naar de testomgeving of productieomgeving. | Automatisch opnemen | <ul><li>Ontwikkelen</li><li>Extensies beheren</li></ul> | <ul><li>Eigenschappen beheren</li></ul> |
| De Mobile App Developer | Is verantwoordelijk voor de implementatie van Adobe- en oplossingen van derden in een systeemeigen mobiele app. | Automatisch opnemen | <ul><li>Ontwikkelen</li><li>Extensies beheren</li></ul> | <li>Eigenschappen beheren</li><li>App Configurations beheren</li> |
| Het IT-team | Wijzig eigenlijk geen markeringen, maar zij hebben volledige controle over de het opvoeren en productiemilieu&#39;s en wat in hen is. | Automatisch opnemen | (Geen) | <ul><li>Goedkeuren</li><li>Publicatie</li><li>Omgevingen beheren</li></ul> |
| Extensieontwikkelaar | Hiermee ontwikkelt u extensies en kunt u deze ter goedkeuring verzenden, maar u kunt ze niet publiceren of toevoegen aan bestaande eigenschappen. | Automatisch opnemen | <ul><li>Ontwikkelen</li></ul> | <ul><li>Eigenschappen beheren</li><li>Extensies ontwikkelen</li></ul> |
| De supergebruiker | Doe alles. | Automatisch opnemen | <ul><li>Ontwikkelen</li><li>Goedkeuren</li><li>Publicatie</li><li>Extensies beheren</li><li>Omgevingen beheren</li></ul> | <ul><li>Eigenschappen beheren</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Volgende stappen

Dit document bevat een overzicht van de beschikbare machtigingen voor tags in Experience Platform. Raadpleeg de handleiding voor informatie over het configureren van productprofielen voor tags in Adobe Admin Console [het beheren van gebruikerstoestemmingen voor gegevensinzameling](../../../collection/permissions.md).
