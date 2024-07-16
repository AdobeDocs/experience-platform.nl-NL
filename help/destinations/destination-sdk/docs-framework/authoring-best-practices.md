---
title: Aanbevolen werkwijzen ontwerpen
description: Leer welke regels en tips u moet volgen wanneer u de pagina met doeldocumentatie ontwerpt, om te controleren of deze voldoet aan de kwaliteitsnormen voor Adobe Experience Platform-documentatie.
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# Aanbevolen werkwijzen ontwerpen

## Overzicht {#overview}

Deze pagina beschrijft regels die u zou moeten volgen wanneer [ creërend uw pagina van de bestemmingsdocumentatie ](./documentation-instructions.md), om ervoor te zorgen dat het aan de normen van de documentatiekwaliteit van Adobe Experience Platform voldoet.

## Algemene richtsnoeren {#general-guidance}

* Wanneer het invullen van het [ malplaatje ](./self-service-template.md) voor uw bestemmingsdocumentatie, verwijs naar de gids van de Adobe contribuant voor informatie over [ het verbinden ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html), [ lijsten ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#tables), de [ gesteunde prijsdalingssyntaxis ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html), [ het schrijven van begeleiding ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html), en meer.
* Plaats geen opmerkingen en schattingen in de productdocumentatie.
* In de documentatie van het Experience Platform, gebruiken de schrijvers van de Adobe **vette het formatteren** om naar gebruikersinterfacecontroles, als dit te verwijzen:
   * Ga naar **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** en selecteer de tab **[!UICONTROL Catalog]** . Bekijk een voorbeeld van hoe de controles van het gebruikersinterface in a [ bestemmingsleerprogramma ](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#select-destination) worden gedocumenteerd.

## Schrijfstijl

>[!IMPORTANT]
>
>Lees [ het Schrijven begeleiding voor de Documentatie van de Adobe ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html) alvorens u begint de pagina van de bestemmingsdocumentatie te ontwerpen.

* Houd je zinnen kort en kom snel op. Als uw zin langer is dan 20 woorden of meerdere komma&#39;s gebruikt, kunt u het opsplitsen in aparte zinnen. Zinnen van meer dan 20 woorden kunnen vooral lastig zijn voor lezers.
* Wees niet al te beleefd. Vermijd het gebruik van &quot;alstublieft&quot; of &quot;vriendelijk ...&quot; in technische documentatie.

## Koppelen {#linking}

Volg de meegeleverde documentatiesjabloon en bewerk de bestaande koppelingen in de sjabloon niet. Wanneer het omvatten van nieuwe verbindingen, lees [ gebruikend verbindingen in documentatie ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html) in de bijdragegids.

## Richtlijnen voor branding {#branding}

* AEP is geen erkende publieke term. Gebruik Adobe Experience Platform voor het eerste gebruik, dan Experience Platform en vervolgens Platform.
   * **gebruik niet**: Alvorens u gegevens van AEP naar YourDestination kunt uitvoeren, zorg ervoor u leest en deze eerste vereisten voltooit.
   * **Gebruik**: Alvorens u gegevens van Adobe Experience Platform naar YourDestination kunt uitvoeren, zorg ervoor u leest en deze eerste vereisten voltooit.

## Afbeeldingen en screenshots {#images-and-screenshots}

* Voor informatie over [ hoe te om aan beelden ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#images) te verbinden, verwijs naar de bijdragegids.
* Wanneer het gebruiken van screenshots, gelieve ervoor te zorgen dat uw screenshot het volledige scherm van Platform UI vangt.
* Wanneer u afbeeldingen markeert om een bepaald besturingselement of label op de pagina te markeren, probeert u de markeringsstijl te volgen die wordt gebruikt door het documentatieteam van het Experience Platform. Bericht hoe op profiel-gebaseerd in [ dit schermafbeelding ](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency) wordt benadrukt.
* Gebruik afbeeldingen in de `png` -indeling.
* Gebruik geen genummerde schermafbeeldingen als bestandsnamen. Namen van afbeeldingsbestanden moeten beschrijvend zijn.
   * **gebruikt niet**: `1.png`, `2.png`, `3.png`
   * **Gebruik**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* Gebruik alt-tekst voor alle afbeeldingen die u aan de documentatie toevoegt en gebruik de juiste grammatica in de alt-tekst.
   * **gebruikt niet**: De details van de bestemmingsverbinding
   * **Gebruik**: Beeld van het Platform UI, tonend de details van de bestemmingsverbinding die in worden gevuld.

## Proces {#process}

* Het [ documentatiemalplaatje ](./self-service-template.md) wordt bijgewerkt niet vaak, gebaseerd op partner terugkoppelt. Alvorens u met het ontwerpen van documentatie voor uw bestemming begint, zorg ervoor dat u de [ recentste versie van het malplaatje ](../assets/docs-framework/yourdestination-template.zip) hebt gedownload.
* Auteur de documentatie en creeer het verzoek van de documentatietrek (PR) van een tak in uw vork *buiten de belangrijkste tak*. Verwijs naar voorlegt bestemming voor overzichtssectie wanneer het ontwerpen in de [ interface GitHub ](./use-github-interface-to-create-documentation.md#submit-review) of in [ uw lokaal milieu ](./work-in-local-environment.md#submit-review).
