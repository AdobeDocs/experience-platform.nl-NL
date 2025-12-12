---
title: Properties
description: Leer hoe uw extensies, omgevingen en bibliotheken zijn georganiseerd en gegroepeerd voor uw organisatie in Adobe Experience Platform.
exl-id: e5b4a853-c23e-498c-9e20-e773ea1de88b
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 0%

---

# Properties

## Web-eigenschappen

Een webeigenschap is een verzameling regels, gegevenselementen, geconfigureerde extensies, omgevingen en bibliotheken.  Elke webeigenschap heeft een eigen set insluitcodes en kan worden geïmplementeerd op een willekeurig aantal verschillende websites (verschillende domeinen).

## Mobiele eigenschappen

Een eigenschap van het type mobile kan meerdere toepassingen bevatten. In een mobiele eigenschap kunt u bijvoorbeeld dezelfde set regels en extensies beheren voor meerdere iOS- en Android-toepassingen.

## Aanbevolen procedures voor het plannen van eigenschappen {#best-practices-for-planning-properties}

Elke implementatie van tags in Adobe Experience Platform kan heel anders zijn. Ze hebben een groot aantal verschillende behoeften op het gebied van gegevensverzameling, variabel gebruik, extensies, tags van derden, andere systemen en technologieën, mensen, teams, geografische regio&#39;s enzovoort. U moet de eigenschappen zodanig structureren dat deze overeenkomen met de workflow en processen van uw organisatie.

Houd rekening met het volgende wanneer u eigenschappen plant:

* Codestructuur
* Gegevens
* Variabelen
* Extensies, codes en systemen
* Mensen

### Codestructuur

Sites zijn gebaseerd op HTML en mobiele toepassingen op code.  Als de onderliggende HTML-sjablonen of -codebases hetzelfde zijn voor meerdere sites en toepassingen, kunt u overwegen één tag-eigenschap te gebruiken om meerdere sites of apps te beheren.

### Gegevens

Zijn de gegevens die u gaat verzamelen voor al uw websites of toepassingen erg vergelijkbaar, enigszins vergelijkbaar of uniek?

Als de gegevens u moet verzamelen gelijkaardig zijn, zou het steek kunnen zijn om die plaatsen of toepassingen in één bezit te groeperen om het dupliceren van regels of het kopiëren van regels van één bezit aan een andere te vermijden.

Als uw gegevensinzamelingsbehoeften voor elke plaats of toepassing uniek zijn, zou het zinvol kunnen zijn om hen in hun eigen eigenschappen te scheiden. Met deze methode kunt u de gegevensverzameling specifieker beheren, zonder grote hoeveelheden voorwaardelijke logica te gebruiken in aangepaste scripts.

### Variabelen

Gelijkaardig aan gegevens, gaan de variabelen u in uw [!DNL Analytics] en andere uitbreidingen zeer gelijkaardig, enigszins gelijkaardig, of uniek plaatsen?

Als eVar27 bijvoorbeeld wordt gebruikt voor dezelfde bronwaarde op al uw websites of toepassingen, is het verstandig om die sites of toepassingen te groeperen, zodat u die algemene variabelen in slechts één eigenschap kunt instellen.

### Extensies, codes en systemen

Zijn de uitbreidingen, de markeringen, en de systemen u gaat opstellen zeer gelijkaardig, enigszins gelijkaardig, of uniek?

Als de uitbreidingen, de markeringen, en de systemen u op uw plaatsen of de toepassingen zult opstellen zeer gelijkaardig zijn, zou u hen in het zelfde bezit kunnen willen omvatten.

Als u [!DNL Adobe Analytics] op slechts één plaats of toepassing opstelt, en uw andere uitbreidingen en markeringen ook uniek zijn, zou u afzonderlijke eigenschappen kunnen willen tot stand brengen zodat u meer controle hebt.

Als u bijvoorbeeld [!DNL Adobe Analytics] , [!DNL Target] en dezelfde extensies van derden implementeert voor al uw sites of toepassingen, is dat een reden om ze samen te groeperen.

### Mensen

Voor de personen, teams en organisaties die in Adobe Experience Platform werken, hebben ze toegang nodig tot al uw websites en toepassingen, sommige of slechts één.

De eigenschappen van het Beheer van de Gebruiker staan u toe om verschillende rollen aan verschillende mensen voor elk van uw eigenschappen, of op een per-bezitsbasis toe te wijzen. Als iemand voldoende rechten heeft, kan die persoon administratieve handelingen uitvoeren op alle eigenschappen in die Experience Platform-organisatie. Alle andere rollen kunnen op een per-bezitsbasis worden toegewezen. U kunt zelfs een bezit voor bepaalde gebruikers (niet-admins) verbergen door hen geen rol in dat bezit te geven.

## Eigenschappenpagina

Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Voor het web is er slechts één code voor het insluiten van publicatie per eigenschap. Voor mobiele apparaten is er één configuratie-toepassings-id per eigenschap.

Een eigenschap kan elke groepering van een of meer domeinen en subdomeinen zijn. U kunt deze elementen op dezelfde manier beheren en bijhouden. Stel dat u meerdere websites hebt die op één sjabloon zijn gebaseerd en dat u dezelfde elementen op alle websites wilt bijhouden. U kunt één eigenschap toepassen op meerdere domeinen.

De linkerkant van het scherm toont de bedrijven in uw organisatie. Dit is vooral handig als u meerdere accounts beheert. Selecteer een bedrijf om de eigenschappen en de controlelogboeken voor dat bedrijf te zien.

Elke eigenschap wordt weergegeven in de lijst Eigenschappen.

De lijst Eigenschappen bevat de volgende informatie:

* Eigenschapnaam
* Platform
* Status

Selecteer een eigenschap om een overzicht van die eigenschap weer te geven. In het overzicht worden alle activiteiten weergegeven die op de eigenschap zijn uitgevoerd. Ook worden de metriek en extensies voor de eigenschap weergegeven.

## Een eigenschap maken of configureren

Deze sectie biedt richtlijnen voor het maken of configureren van een tag-eigenschap in Adobe Experience Platform.

>[!NOTE]
>
>Alleen gebruikers met voldoende rechten kunnen een eigenschap maken. Zie [ Gebruikersbeheer ](user-permissions.md).

Alvorens te beginnen, herzie [ Beste praktijken voor het plannen van eigenschappen ](companies-and-properties.md#best-practices-for-planning-properties) voor eigenschappen.

Navigeer naar de pagina van uw bedrijf en selecteer vervolgens **[!UICONTROL Add Property]** of selecteer een bestaande eigenschap in de lijst en selecteer **[!UICONTROL Configure]** .

![](../../images/property-settings.png)

### Voor web

Volg de instructies om een webeigenschap te maken.

1. Vul de velden in:

   **Naam:** De naam van uw bezit.

   **Domeinen:** de basis URL van om het even welke plaatsen u van plan bent om dit bezit aan op te stellen

1. (Geavanceerd) **[!UICONTROL Run rule components in sequence]** Schakel dit selectievakje in om de voorwaarden en handelingen te laten wachten totdat de vorige zijn voltooid voordat ze worden uitgevoerd
1. (Geavanceerd) **[!UICONTROL Return an empty string for missing data elements:]** Als u naar een gegevenselement verwijst dat niet in een bibliotheek bestaat, wordt `undefined` normaal gesproken geretourneerd. Schakel dit selectievakje in als u wilt dat dat scenario een lege tekenreeks retourneert.
1. (Geavanceerd) **[!UICONTROL Configure for extension development:]** Schakel dit selectievakje in als u ontwikkelextensies wilt installeren die actief door uw bedrijf worden ontwikkeld
1. Selecteer **[!UICONTROL Save]**.

### Voor mobiel

Volg de instructies om een eigenschap mobile te maken.

1. Vul de velden in:

   * **Naam:** De naam van uw bezit.
   * **Privacy:** Door gebrek wordt het privacy plaatsen geplaatst aan Opted binnen, betekenend dat u voor SDK gegevens zou willen verzamelen en verzenden naar oplossingen. Als u Opted Out selecteert, verzendt de SDK standaard GEEN gegevens naar oplossingen. Als u Onbekend kiest als instelling, vereist de SDK dat de toepassing de gebruiker eerst vraagt om gegevensverzameling en -deling toe te staan.

     >[!NOTE]
     >
     >Deze instellingen kunnen verder worden beheerd via de API in de mobiele toepassing.

   * **HTTPS van het Gebruik:** kies als alle gegevensmededeling over HTTP of HTTPS zou moeten worden verzonden.

1. Selecteer **[!UICONTROL Save]**.

Nadat uw bezit wordt gecreeerd, voegt Experience Platform automatisch een standaardgastheer, een reeks milieu&#39;s (Ontwikkeling, het Opvoeren, en Productie), en de standaarduitbreidingen toe.

## Een eigenschap verwijderen

Voer de onderstaande stappen uit om een eigenschap tag te verwijderen.

>[!NOTE]
>
>Verwijderen van eigenschap kan niet worden teruggedraaid. De aanvrager moet een gebruiker op beheerdersniveau zijn. Deze aanvraag kan niet ongedaan worden gemaakt.

1. Selecteer in de lijst Eigenschappen de eigenschap die u wilt verwijderen.

   U kunt meerdere eigenschappen selecteren om te verwijderen.

1. Selecteer **[!UICONTROL Delete]** en bevestig vervolgens de verwijdering van de eigenschap.
