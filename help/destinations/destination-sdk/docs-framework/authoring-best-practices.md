---
title: Aanbevolen werkwijzen ontwerpen
description: Leer welke regels en tips u moet volgen wanneer u de pagina met doeldocumentatie ontwerpt, om te controleren of deze voldoet aan de kwaliteitsnormen voor Adobe Experience Platform-documentatie.
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: 0b9b724c2530e43ce681011d12fc1341148ddbf5
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# Aanbevolen werkwijzen ontwerpen

## Overzicht {#overview}

Op deze pagina worden de regels beschreven die u moet volgen wanneer [ontwerpen van de doeldocumentatie](./documentation-instructions.md) pagina, om ervoor te zorgen dat deze voldoet aan de kwaliteitsnormen voor documentatie van Adobe Experience Platform.

## Algemene richtsnoeren {#general-guidance}

* Wanneer u de [template](./self-service-template.md) voor uw bestemmingsdocumentatie, verwijs naar de Adobe contributor gids voor informatie over [koppelen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en), [tabellen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#tables)de [ondersteunde markeringssyntaxis](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en), [schrijfbegeleiding](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en)en meer.
* Plaats geen opmerkingen en schattingen in de productdocumentatie.
* In de documentatie van het Experience Platform, gebruiken de schrijvers van Adobe **vet opmaken** om naar gebruikersinterfacecontroles te verwijzen, als dit:
   * Ga naar **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** en selecteert u de **[!UICONTROL Catalog]** tab. Bekijk een voorbeeld van hoe de controles van het gebruikersinterface in a worden gedocumenteerd [zelfstudie over doelen](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#select-destination).

## Schrijfstijl

>[!IMPORTANT]
>
>Lezen [Richtlijnen voor het schrijven van Adobe-documentatie](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) voordat u begint met het ontwerpen van de pagina met doeldocumentatie.

* Houd je zinnen kort en kom snel tot het punt. Als uw zin langer is dan 20 woorden of meerdere komma&#39;s gebruikt, kunt u het opsplitsen in aparte zinnen. Zinnen van meer dan 20 woorden kunnen vooral lastig zijn voor lezers.
* Wees niet al te beleefd. Vermijd het gebruik van &quot;alsjeblieft&quot; of &quot;aardig doen ...&quot; in technische documentatie.

## Koppeling {#linking}

Volg de meegeleverde documentatiesjabloon en bewerk de bestaande koppelingen in de sjabloon niet. Lees bij het opnemen van nieuwe koppelingen [gebruiken van verbindingen in documentatie](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en) in de handleiding voor contribuanten.

## Richtlijnen voor branding {#branding}

* AEP is geen erkende publieke term. Gebruik Adobe Experience Platform voor het eerste gebruik, Experience Platform en Platform.
   * **Niet gebruiken**: Voordat u gegevens kunt exporteren van AEP naar YourDestination, moet u controleren of u deze voorwaarden hebt gelezen en voltooid.
   * **Gebruiken**: Voordat u gegevens kunt exporteren van Adobe Experience Platform naar YourDestination, moet u controleren of aan deze voorwaarden is voldaan.

## Afbeeldingen en schermafbeeldingen {#images-and-screenshots}

* Voor informatie over [hoe te om aan beelden te verbinden](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#images), raadpleegt u de handleiding voor contribuanten.
* Wanneer het gebruiken van screenshots, gelieve ervoor te zorgen dat uw het volledige scherm UI van het Platform vangt.
* Wanneer u afbeeldingen markeert om een bepaald besturingselement of label op de pagina te markeren, probeert u de markeringsstijl te volgen die wordt gebruikt door het documentatieteam van het Experience Platform. Let op: Profiel gebaseerd in [deze screenshot](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* Gebruik `png` afbeeldingen opmaken.
* Gebruik geen genummerde schermafbeeldingen als bestandsnamen. Namen van afbeeldingsbestanden moeten beschrijvend zijn.
   * **Niet gebruiken**: `1.png`, `2.png`, `3.png`
   * **Gebruiken**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* Gebruik alt-tekst voor alle afbeeldingen die u aan de documentatie toevoegt en gebruik de juiste grammatica in de alt-tekst.
   * **Niet gebruiken**: Gegevens doelverbinding
   * **Gebruiken**: Afbeelding van de interface van het Platform, waarin gegevens over de doelverbinding zijn ingevuld.

## Proces {#process}

* De [documentatiesjabloon](./self-service-template.md) wordt niet regelmatig bijgewerkt, gebaseerd op partner terugkoppelt. Voordat u begint met het ontwerpen van documentatie voor uw bestemming, moet u controleren of u het gereedschap [laatste versie van de sjabloon](/help/destinations/destination-sdk/docs-framework/assets/yourdestination-template.zip).
* Maak de documentatie en maak de documentatie (PR) van een tak in uw vork. *andere dan het hoofdbijkantoor*. Verwijs naar de verzendbestemming voor overzichtssectie wanneer creatie in [GitHub-interface](./use-github-interface-to-create-documentation.md#submit-review) of in [uw lokale omgeving](./work-in-local-environment.md#submit-review).
